> Let’s go step-by-step to **understand `.gitlab-ci.yml`**, its **structure**, and then build a **real-world Java CI/CD pipeline** that:

* Builds a **Maven Java application**
* Builds a **Docker image**
* Pushes it to a **GitLab Container Registry**
* Deploys it to **Kubernetes (K8s)**

---

## 🔹 1. What is `.gitlab-ci.yml`?

`.gitlab-ci.yml` is the **pipeline definition file** for GitLab CI/CD.
It tells GitLab **what to do, when to do it, and on which runner**.

GitLab looks for this file in the **root** of your repository.

---

## 🔹 2. Structure of `.gitlab-ci.yml`

Here’s the **key structure** of the file:

```yaml
stages:              # Defines the order of execution
  - build
  - test
  - package
  - docker
  - deploy

variables:           # Global variables
  MAVEN_CLI_OPTS: "-s .m2/settings.xml --batch-mode"
  DOCKER_DRIVER: overlay2
  IMAGE_TAG: "$CI_REGISTRY_IMAGE:$CI_COMMIT_SHORT_SHA"

before_script:       # Common setup commands before all jobs
  - echo "Starting job for $CI_PROJECT_NAME"
  - echo "Current branch: $CI_COMMIT_REF_NAME"

build_job:           # Job name
  stage: build       # Stage it belongs to
  script:            # Commands to run
    - mvn $MAVEN_CLI_OPTS clean compile
  artifacts:         # Files to pass to next stage
    paths:
      - target/

test_job:
  stage: test
  script:
    - mvn $MAVEN_CLI_OPTS test

package_job:
  stage: package
  script:
    - mvn $MAVEN_CLI_OPTS package -DskipTests
  artifacts:
    paths:
      - target/*.jar

docker_build_job:
  stage: docker
  image: docker:latest
  services:
    - docker:dind
  script:
    - docker login -u "$CI_REGISTRY_USER" -p "$CI_REGISTRY_PASSWORD" $CI_REGISTRY
    - docker build -t $IMAGE_TAG .
    - docker push $IMAGE_TAG

deploy_job:
  stage: deploy
  image: bitnami/kubectl:latest
  script:
    - kubectl config use-context $KUBE_CONTEXT
    - kubectl set image deployment/java-webapp java-webapp=$IMAGE_TAG
    - kubectl rollout status deployment/java-webapp
  only:
    - main
```

---

## 🔹 3. Explanation of Key Sections

| Section              | Purpose                                                                |
| -------------------- | ---------------------------------------------------------------------- |
| **stages**           | Defines pipeline phases in sequence (build → test → deploy).           |
| **variables**        | Stores reusable environment variables (image tags, credentials, etc.). |
| **before_script**    | Runs before each job — typically used for setup.                       |
| **jobs**             | Each logical task (build, test, deploy) is a job.                      |
| **image & services** | Defines Docker image to use and services like Docker-in-Docker (dind). |
| **artifacts**        | Files to be preserved between jobs (e.g., `.jar` file).                |
| **only/except**      | Controls when jobs run (e.g., only on `main` branch).                  |

---

## 🔹 4. Real-Life Example — Java App → Docker → Kubernetes

**Assume:**

* Java app built using Maven
* GitLab Container Registry used to store image
* Kubernetes cluster (EKS/AKS/GKE) used for deployment
* You’ve added Kube credentials in **GitLab → Settings → CI/CD → Variables**

---

### 🧱 Directory Structure

```
java-deepak-webapp/
├── .gitlab-ci.yml
├── Dockerfile
├── pom.xml
├── src/
└── k8s/
    └── deployment.yaml
```

---

### 🧩 Dockerfile

```Dockerfile
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/java-deepak-webapp.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]
```

---

### 🧩 Kubernetes Deployment (`k8s/deployment.yaml`)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: java-webapp
  namespace: devops
spec:
  replicas: 2
  selector:
    matchLabels:
      app: java-webapp
  template:
    metadata:
      labels:
        app: java-webapp
    spec:
      containers:
      - name: java-webapp
        image: registry.gitlab.com/deepak/java-deepak-webapp:latest
        ports:
        - containerPort: 8080
```

---

### 🧩 `.gitlab-ci.yml` — Real CI/CD Example

```yaml
stages:
  - build
  - test
  - package
  - docker
  - deploy

variables:
  IMAGE_TAG: "$CI_REGISTRY_IMAGE:$CI_COMMIT_SHORT_SHA"
  K8S_NAMESPACE: "devops"

before_script:
  - echo "Running pipeline for $CI_PROJECT_NAME"
  - echo "Current branch: $CI_COMMIT_REF_NAME"

build_job:
  stage: build
  image: maven:3.9.6-eclipse-temurin-17
  script:
    - mvn clean compile

test_job:
  stage: test
  image: maven:3.9.6-eclipse-temurin-17
  script:
    - mvn test

package_job:
  stage: package
  image: maven:3.9.6-eclipse-temurin-17
  script:
    - mvn package -DskipTests
  artifacts:
    paths:
      - target/*.jar

docker_build:
  stage: docker
  image: docker:latest
  services:
    - docker:dind
  script:
    - docker login -u "$CI_REGISTRY_USER" -p "$CI_REGISTRY_PASSWORD" $CI_REGISTRY
    - docker build -t $IMAGE_TAG .
    - docker push $IMAGE_TAG
  only:
    - main

deploy_to_k8s:
  stage: deploy
  image: bitnami/kubectl:latest
  script:
    - kubectl config use-context $KUBE_CONTEXT
    - kubectl -n $K8S_NAMESPACE set image deployment/java-webapp java-webapp=$IMAGE_TAG
    - kubectl -n $K8S_NAMESPACE rollout status deployment/java-webapp
  only:
    - main
```

---

## 🔹 5. Real-life Flow (How it runs)

1. **Developer pushes code → GitLab detects `.gitlab-ci.yml`**
2. **Pipeline starts:**

   * 🧱 **Build job:** compiles Java code
   * 🧪 **Test job:** runs unit tests
   * 📦 **Package job:** creates `.jar`
   * 🐳 **Docker job:** builds image, pushes to GitLab Registry
   * ☸️ **Deploy job:** updates Kubernetes Deployment with new image
3. **K8s pulls new image → new pods deployed automatically**

---

## 🔹 6. Example Output in GitLab Pipeline UI

| Stage   | Job           | Status   | Description                 |
| ------- | ------------- | -------- | --------------------------- |
| Build   | build_job     | ✅ Passed | Code compiled successfully  |
| Test    | test_job      | ✅ Passed | All unit tests passed       |
| Package | package_job   | ✅ Passed | WAR/JAR packaged            |
| Docker  | docker_build  | ✅ Passed | Image pushed to registry    |
| Deploy  | deploy_to_k8s | ✅ Passed | New version deployed to K8s |

---

Would you like me to show you the **same example** but configured with **GitLab variables (like `$KUBE_CONFIG`, `$CI_REGISTRY_IMAGE`) and Kubernetes Secret integration** (for production-ready setup)?
That would make it **ready for your real cluster deployment**.

> Let’s create a **simple beginner-friendly GitLab CI/CD pipeline** for any small project (for example, just a few text files or scripts).

We’ll go step-by-step so you can **see it working directly in GitLab**.

---

## 🧭 GOAL

You’ll:

* Create a **simple GitLab project**
* Add a `.gitlab-ci.yml`
* See a **pipeline with build → test → deploy** stages run automatically
  (no Docker, no Java, no Kubernetes)

---

## 🔹 Step 1: Create a New GitLab Project

1. Go to your GitLab dashboard → click **“New Project”**
2. Choose **“Create blank project”**
3. Name it something like → `gitlab-simple-ci`
4. Leave visibility **Private** or **Public**
5. Click **Create Project**

---

## 🔹 Step 2: Add a Simple File

In your repository, create a new file called `hello.sh`:

**File: `hello.sh`**

```bash
#!/bin/bash
echo "Hello Deepak, GitLab CI/CD is running successfully!"
```

Then make sure it’s executable:

```bash
chmod +x hello.sh
```

---

## 🔹 Step 3: Create `.gitlab-ci.yml`

In the same repository, create a new file named:

**File:** `.gitlab-ci.yml`

---

## 🔹 Step 4: Add This Simple CI/CD Configuration

```yaml
stages:
  - build
  - test
  - deploy

build_job:
  stage: build
  script:
    - echo "🔧 Building the project..."
    - mkdir build
    - echo "Build completed successfully!" > build/build_output.txt
  artifacts:
    paths:
      - build/

test_job:
  stage: test
  script:
    - echo "🧪 Running tests..."
    - if [ -f build/build_output.txt ]; then echo "Test passed ✅"; else echo "Test failed ❌" && exit 1; fi

deploy_job:
  stage: deploy
  script:
    - echo "🚀 Deploying application..."
    - echo "Deployed successfully by GitLab CI/CD!"
  only:
    - main
```

---

## 🔹 Step 5: Commit and Push

If you’re editing directly in GitLab, click **Commit Changes**.
Or if you’re using local Git:

```bash
git add .
git commit -m "Added simple GitLab CI pipeline"
git push origin main
```

---

## 🔹 Step 6: View Pipeline in GitLab

Now go to your GitLab project:

➡️ **CI/CD → Pipelines**

You’ll see something like:

```
build → test → deploy
```

Each job runs automatically on GitLab’s shared runner.

✅ **Expected output:**

* The `build_job` creates a `build/build_output.txt` file
* The `test_job` checks that file exists
* The `deploy_job` prints “Deployed successfully…”

---

## 🔹 Step 7: View Job Logs

Click each job → **“Trace”**
You’ll see logs like this:

```
Running with gitlab-runner 17.x.x ...
$ echo "🔧 Building the project..."
🔧 Building the project...
Build completed successfully!
```

---

## 🔹 Step 8: Confirm the Artifacts

In the **build job**, GitLab stores the generated file `build_output.txt` as an **artifact**.
You can download it from the **Job → Artifacts → Browse** tab.

---

## 🔹 Step 9: Understand the Structure

| Section      | Description                         |
| ------------ | ----------------------------------- |
| `stages`     | Defines the order of execution      |
| `build_job`  | Builds or prepares files            |
| `test_job`   | Runs simple tests                   |
| `deploy_job` | Simulates a deployment              |
| `artifacts`  | Files preserved for later stages    |
| `only: main` | Restricts deploy to the main branch |

---

## 🔹 Step 10: Expand Later

Once this works, you can:

* Replace `echo` with real commands (`python main.py`, `mvn test`, etc.)
* Add environment-specific deploy stages
* Introduce Docker builds or K8s deployments later

---

✅ **End Result:**
You’ve now got a **working GitLab CI/CD pipeline** that:

* Runs automatically on each push
* Executes multiple stages
* Produces visible logs and artifacts

---

Would you like me to show the **next-level version** of this same simple pipeline — where we add a **Python app** (like `app.py`) and make GitLab run and test it automatically?
That’s the perfect next step after this one.

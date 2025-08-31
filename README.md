# Roadmap

# 📘 GitLab CI/CD Roadmap & Syllabus (Module-Wise)

---

## **Module 1: GitLab Basics & Setup**

🔹 *Goal*: Get familiar with GitLab ecosystem before diving into pipelines.

**Topics:**

* Git vs GitLab (self-hosted vs SaaS)
* GitLab repositories, groups, and projects
* GitLab Runners (shared vs specific)
* GitLab Permissions & Roles
* Installing GitLab Runner on Linux/Windows/Docker

**Practical Exercises:**

* Create GitLab account & new repository
* Setup GitLab Runner locally (shell, docker executors)
* Add `.gitlab-ci.yml` file to repo

**Mini Projects (3):**

1. Create GitLab repo + push sample code (Python/Node.js/Java).
2. Setup GitLab Runner in Docker and verify pipeline run.
3. Fork open-source repo and run your own GitLab pipeline.

---

## **Module 2: GitLab CI/CD Fundamentals**

🔹 *Goal*: Learn pipeline syntax & execution.

**Topics:**

* `.gitlab-ci.yml` structure (stages, jobs, scripts)
* Artifacts, Cache, Variables
* Pipeline Visualization (DAGs, dependencies)
* Manual jobs & rules
* Pipeline security basics

**Practical Exercises:**

* Create pipelines with `build → test → deploy` stages
* Use variables, artifacts, caching
* Add manual approvals

**Mini Projects (3):**

1. CI pipeline for a simple Java Maven/Gradle app.
2. Node.js pipeline with linting + unit testing.
3. Python Flask app pipeline (pytest + packaging).

---

## **Module 3: Advanced Pipelines**

🔹 *Goal*: Master advanced features.

**Topics:**

* Multi-stage & multi-environment pipelines
* Conditional jobs (`rules: if`)
* Pipeline templates & `include`
* Dynamic pipelines with YAML anchors
* Parallelization (matrix builds)
* Scheduled pipelines

**Practical Exercises:**

* Write pipeline with dev/test/prod stages
* Trigger child pipelines from parent
* Use YAML templates for multiple services

**Mini Projects (3):**

1. Multi-stage pipeline for microservices (frontend + backend).
2. Build matrix for Python versions (3.8, 3.9, 3.10).
3. Create reusable pipeline templates for multiple projects.

---

## **Module 4: GitLab CI/CD for Deployments**

🔹 *Goal*: Deploy real applications.

**Topics:**

* GitLab Environments & Deployments
* Deploy tokens & SSH keys
* GitLab Pages (static sites)
* Docker in GitLab pipelines
* GitLab Registry (push/pull images)

**Practical Exercises:**

* Deploy static website to GitLab Pages
* Build & push Docker images to GitLab Registry
* Deploy app to a remote Linux server with SSH

**Mini Projects (3):**

1. Build Docker image for Node.js app + push to GitLab Registry.
2. Deploy Flask app on VM using GitLab pipeline.
3. Deploy Java WAR file to Tomcat using GitLab pipeline.

---

## **Module 5: Integrations with DevOps Tools**

🔹 *Goal*: Integrate GitLab with ecosystem tools.

**Topics:**

* GitLab + Docker (build/push images)
* GitLab + Kubernetes (Auto DevOps, Helm, K8s integration)
* GitLab + AWS (EC2, S3, Lambda)
* GitLab + Azure (Web Apps, AKS)
* GitLab + GCP (Cloud Run, GKE)
* GitLab + Ansible/Terraform/Jenkins

**Practical Exercises:**

* Setup GitLab → Kubernetes cluster integration
* Deploy infra with Terraform via GitLab CI/CD
* Trigger Jenkins pipeline from GitLab CI

**Mini Projects (3):**

1. Deploy microservice app to Kubernetes using GitLab CI/CD.
2. Provision AWS EC2 using Terraform via GitLab pipeline.
3. Configure GitLab pipeline to trigger Jenkins job.

---

## **Module 6: GitLab Security & DevSecOps**

🔹 *Goal*: Secure pipelines & integrate security tools.

**Topics:**

* GitLab Security Scanning (SAST, DAST, Dependency Scanning)
* Container Scanning
* Secret Detection
* Compliance & Audit features

**Practical Exercises:**

* Enable SAST for Python/Java project
* Run DAST against a deployed app
* Configure GitLab to block merge on security findings

**Mini Projects (3):**

1. Secure CI/CD for Java Maven project (SAST + Dependency Scanning).
2. Container image scanning for Dockerized app.
3. DAST scanning on deployed Flask app.

---

## **Module 7: Monitoring & Optimization**

🔹 *Goal*: Make pipelines efficient and observable.

**Topics:**

* Pipeline duration optimization (caching, parallel jobs)
* Retry & failure strategies
* GitLab CI/CD with Prometheus & Grafana
* GitLab CI/CD for logging (ELK Stack)

**Practical Exercises:**

* Optimize pipelines with caching
* Monitor pipelines with Prometheus
* Store logs centrally

**Mini Projects (3):**

1. CI/CD pipeline with caching enabled for Maven builds.
2. GitLab → Prometheus/Grafana integration.
3. Log GitLab pipeline data into ELK Stack.

---

## **Module 8: Real-Time Enterprise Projects**

🔹 *Goal*: Work like in real companies.

**End-to-End Projects:**

1. **E-commerce App CI/CD**

   * Multi-service (frontend, backend, DB)
   * Docker build + push → Kubernetes deploy → Monitoring

2. **Banking App CI/CD (DevSecOps)**

   * Java + Flask services
   * SAST + DAST + Terraform + Kubernetes

3. **Hybrid Cloud Deployment**

   * Deploy app to AWS (EC2 + S3) & Azure (Web Apps) via GitLab pipelines

---

# 🚀 Roadmap Flow

1. **Module 1–2:** Basics (setup & simple pipelines) → (\~2 weeks)
2. **Module 3–4:** Advanced Pipelines & Deployments → (\~3 weeks)
3. **Module 5–6:** Tool Integrations + DevSecOps → (\~3 weeks)
4. **Module 7–8:** Monitoring + Enterprise Projects → (\~2 weeks)

➡️ **Total: 10 weeks (2.5 months)** for mastery with projects.

---

# Syllabus Gitlab CI
Let’s build a **structured, hands-on GitLab CI/CD learning roadmap** that will make you confident enough to build and manage pipelines from scratch — both for personal projects and enterprise DevOps workflows.

Below is a **6-week syllabus** (you can extend it to 8 if you want to go slower).
Each week includes **topics + practical exercises** so you actually *learn by doing*.

---

## 🗓 **GitLab CI/CD Complete Syllabus (6 Weeks)**

---

### **📘 Week 1 – GitLab Basics & Setup**

**Goals:**

* Understand GitLab fundamentals.
* Set up your environment for CI/CD.

**Topics:**

* What is GitLab? Repos, Groups, Projects, Pipelines.
* GitLab vs GitHub.
* Introduction to GitLab Runners.
* Setting up a GitLab account.
* Creating a repository.
* Git basics (clone, commit, push, branch, merge).

**Exercises:**

1. Create a new GitLab account and repository.
2. Clone the repo to your local machine.
3. Add and push a README.md file.
4. Create a new branch and merge it via Merge Request (MR).
5. Explore project settings and CI/CD section.

---

### **⚙️ Week 2 – Getting Started with GitLab CI/CD**

**Goals:**

* Learn pipeline basics and YAML syntax.
* Write your first `.gitlab-ci.yml`.

**Topics:**

* What is CI/CD in GitLab?
* Understanding `.gitlab-ci.yml` structure.
* Jobs, Stages, and Pipelines explained.
* The default pipeline flow.
* Runners: shared vs specific.
* Pipeline visualization.

**Exercises:**

1. Create `.gitlab-ci.yml` with one job that prints “Hello GitLab CI!”
2. Add a `build` stage that echoes “Build started”.
3. Run a pipeline manually and inspect logs.
4. Add a second stage: `test` that checks a simple script (bash script).
5. Make a pipeline run automatically on every push.

---

### **💡 Week 3 – Intermediate CI/CD Concepts**

**Goals:**

* Explore variables, caching, artifacts, and triggers.

**Topics:**

* GitLab CI Variables (predefined, custom, group-level).
* Caching and Artifacts.
* Dependency between jobs.
* Rules vs Only/Except.
* Using Environments and Deployments.
* Manual jobs and `when` keyword.

**Exercises:**

1. Create a pipeline with two stages: build → deploy.
2. Use environment variables in your `.gitlab-ci.yml`.
3. Save build artifacts and download them.
4. Add a manual deploy stage (`when: manual`).
5. Set rules to trigger jobs only on `main` branch.

---

### **🧩 Week 4 – Runners & Advanced Pipelines**

**Goals:**

* Work with your own runner and optimize pipelines.

**Topics:**

* GitLab Runner types and installation.
* Registering a runner (Linux).
* Tags and executors (Shell, Docker, etc.).
* Using Docker in GitLab CI.
* Parallel and matrix builds.
* Child pipelines & includes.
* Pipeline optimization techniques.

**Exercises:**

1. Install a GitLab Runner on your VM.
2. Register the runner with your project.
3. Create a pipeline that runs on your runner only.
4. Use `docker` executor to run a container job.
5. Add a child pipeline to split logic.

---

### **🚀 Week 5 – Continuous Deployment**

**Goals:**

* Deploy code using GitLab CI.

**Topics:**

* GitLab Environments.
* Deployment strategies (manual, auto, review apps).
* Using SSH keys for deployment.
* Deploying to AWS EC2 / Azure VM / GCP (basic setup).
* Using artifacts for deployment.
* GitLab Pages for static site hosting.

**Exercises:**

1. Create a `deploy` stage that copies files via `scp` to a remote server.
2. Deploy a simple HTML site using GitLab Pages.
3. Store deployment credentials securely using CI variables.
4. Add `before_script` and `after_script` sections for setup/cleanup.
5. Visualize environments in GitLab’s UI.

---

### **🔒 Week 6 – Advanced Topics & Real Projects**

**Goals:**

* Integrate GitLab CI with real-world workflows and DevOps tools.

**Topics:**

* Secrets management (Vault integration).
* Using GitLab CI for Docker builds & push to registry.
* Multi-environment (Dev, Staging, Prod) pipelines.
* CI/CD with approval gates.
* Notifications & integrations (Slack, Email).
* Monitoring pipelines.
* Security scans and linting.

**Exercises:**

1. Build and push a Docker image to GitLab Container Registry.
2. Create multi-env pipeline (dev → staging → prod).
3. Use approvals before deploy to prod.
4. Add Slack notifications for failed pipelines.
5. Enable SAST (Static Application Security Testing) in GitLab.

---

## 🧠 **Optional Advanced Weeks (for complete mastery)**

---

### **☸️ Week 7 – GitLab CI with Kubernetes & Auto DevOps**

**Goals:**

* Learn how to connect GitLab CI/CD with Kubernetes.
* Deploy applications automatically using Helm or Auto DevOps.

**Topics:**

* What is Auto DevOps in GitLab.
* Connecting GitLab with a Kubernetes cluster.
* Using GitLab’s Kubernetes integration.
* Deployments using Helm charts.
* Managing secrets for Kubernetes.
* Rolling updates and rollback automation.
* Deployments via GitLab Environments in K8s.

**Exercises:**

1. Create a small Kubernetes cluster (use Minikube, kind, or EKS if available).
2. Connect the cluster to GitLab under **Infrastructure → Kubernetes Clusters**.
3. Deploy a sample web app (e.g., simple Node.js or static site) via GitLab CI.
4. Create a Helm chart for the app and deploy it using a CI job.
5. Add environment-level variables for staging and production.
6. Use GitLab’s built-in Auto DevOps feature and analyze the generated pipeline.
7. Roll out a new version automatically and verify rollback works.

---

### **🤖 Week 8 – GitLab API, GitOps & Automation**

**Goals:**

* Learn to automate GitLab using APIs.
* Implement GitOps principles using GitLab CI.
* Use GitLab CI to trigger or control external systems.

**Topics:**

* GitLab REST & GraphQL APIs overview.
* Automating issues, MRs, and pipelines with API.
* Dynamic pipeline generation via GitLab API.
* Triggering downstream pipelines (multi-repo setup).
* Implementing GitOps-style workflows.
* GitLab Webhooks and integration with external tools.
* CI/CD pipeline governance and best practices.

**Exercises:**

1. Use GitLab API to list your projects and pipelines (via curl or Postman).
2. Write a CI job that triggers another pipeline in a different repo using API token.
3. Automate issue creation when a pipeline fails.
4. Implement a GitOps-style repo where Kubernetes manifests are updated via CI job.
5. Set up a webhook to notify a Slack channel on pipeline completion.
6. Add code quality and linting checks as a separate stage before deployment.
7. Document and version-control your `.gitlab-ci.yml` as a reusable **template** for future projects.

---

## ✅ **After Week 8 — Capstone Project (Highly Recommended)**

**Project Idea:**
Build a full **CI/CD pipeline for a simple web application (Node.js / Java / Python)** that:

* Builds and tests the app.
* Builds a Docker image and pushes it to GitLab Container Registry.
* Deploys to Kubernetes (dev → staging → prod).
* Uses approvals and environment protection.
* Sends Slack notifications on success/failure.

**Bonus:**

* Integrate security scanning (SAST/DAST).
* Use GitLab Pages for documentation.
* Add GitLab API calls for automation.

---



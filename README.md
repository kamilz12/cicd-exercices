# LAB 2 — Cloud Application Programming

## 📌 Objective

Automatically build and publish a Docker container image based on the application from Task 1. The image is published to the **GitHub Container Registry (GHCR)** after passing a security vulnerability scan (CVE).

## ✅ Pipeline Workflow:

1. **Multi-platform Build:** Builds the image for `linux/amd64` and `linux/arm64`.
2. **Caching:** Utilizes DockerHub cache (`mode=max`) to speed up subsequent builds.
3. **Security Audit:** Verifies the image integrity and security using **Trivy**.
4. **Conditional Publishing:** The image is pushed to `ghcr.io` **only if** it contains zero **CRITICAL** or **HIGH** severity vulnerabilities.

## 🧪 Tagging Strategy

* `latest` – Points to the most recent successful build.
* `sha-<commit>` – A unique tag based on the specific Git commit SHA.
* **Cache Location:** `docker.io/<dockerhub-user>/cloud-lab2-cache:latest`

## 🔐 Required Secrets:

Add the following to your repository (Settings > Secrets and variables > Actions):

* `GHCR_PAT` – A GitHub Personal Access Token with `write:packages` permissions.
* `DOCKERHUB_USERNAME` – Your DockerHub login.
* `DOCKERHUB_TOKEN` – A generated access token for DockerHub authentication.

## 🚀 Execution

The workflow is triggered automatically upon committing changes to the `main` branch. It will handle the build, scan, and push processes autonomously.


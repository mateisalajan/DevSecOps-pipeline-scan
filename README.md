# 🚦 DevSecOps Pipeline Demo

This project demonstrates a secure, automated CI/CD pipeline for containerized Python apps. It integrates continuous vulnerability scanning and modern DevSecOps practices using free and open-source tools.

## 📝 Project Overview

- **App:** Simple Python (Flask) microservice, containerized with Docker
- **CI/CD:** Automated with GitHub Actions
- **Security:** All Docker images scanned for vulnerabilities using Trivy
- **Platform:** Local Kubernetes (KinD) for demo, cloud-ready

## 🛡️ Key Features

- **Automated vulnerability scanning:** Every push triggers a Docker image build and a Trivy scan in CI
- **Fail-fast:** CI workflow fails if any CRITICAL or HIGH CVEs are found
- **Extensible:** Designed for further security controls (OPA Gatekeeper, Falco, etc.)

## 🚀 Getting Started

### Prerequisites

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [WSL2](https://docs.microsoft.com/en-us/windows/wsl/) (for Windows users)
- [Git](https://git-scm.com/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [kind](https://kind.sigs.k8s.io/)
- [Helm](https://helm.sh/)

### Setup Steps

1. **Clone the repo:**
   ``` bash
   git clone https://github.com/mateisalajan/DevSecOps-pipeline-scan.git
   cd DevSecOps-pipeline-scan
   ```

2. **Build and run locally:**
   ```bash
   docker build -t sample-app:vuln ./sample-app
   docker run -p 5000:5000 sample-app:vuln
   ```

   Visit [http://localhost:5000](http://localhost:5000) to view the app.

3. **Check automated security scan results:**
   Every commit triggers a GitHub Actions workflow. See [Actions tab](../../actions) for details.

## 🛠️ How It Works

* The pipeline builds your Docker image and scans it with Trivy.
* If CRITICAL or HIGH vulnerabilities are found, the build fails (shift-left security!).
* Results are summarized in [SECURITY\_SCAN\_RESULTS.md](./SECURITY_SCAN_RESULTS.md).

## 📋 Example Security Scan Badge

![Trivy Scan](https://github.com/mateisalajan/DevSecOps-pipeline-scan/actions/workflows/trivy.yml/badge.svg?branch=main)

[See full scan results →](./SECURITY_SCAN_RESULTS.md)

Here’s how you can **summarize your work in the README** for those two steps, with **clear DevSecOps learning outcomes** and room to insert screenshots or CLI output later:

---

## 🛠️ Application Deployment & Policy Enforcement

### 1. Deploying the Application

* **Two image tags were built and pushed:**

  * `sample-app:vuln`: Contains intentional vulnerabilities
  * `sample-app:secure`: Upgraded and remediated, passes Trivy scan
* **Both images deployed to the local Kubernetes cluster using Helm.**

#### Example:

```bash
# Deploy vulnerable version
helm upgrade --install sample-app-vuln ./sample-app --set image.tag=vuln

# Deploy secure version
helm upgrade --install sample-app-secure ./sample-app --set image.tag=secure
```

---

### 2. Gatekeeper Policy Enforcement

* **Gatekeeper installed via Helm:**

  * Enforces Kubernetes Admission Control using OPA/Rego policies.
* **Custom constraint written:**

  * *Blocks any pod whose image tag does not contain `:secure` (i.e., only allows images that passed Trivy scan).*

#### What this demonstrates:

* **Policy-as-Code**: Security policies can be versioned, reviewed, and enforced automatically in CI/CD pipelines.
* **Automated Admission Control:** Vulnerable deployments are denied before they can reach production.

#### Example policy violation (attempt to deploy a vulnerable image):

```bash
$ helm upgrade --install sample-app-vuln ./sample-app --set image.tag=vuln

# Output: No pod created, Gatekeeper denied the deployment!
```

#### Example policy success (deploying the secure image):

```bash
$ helm upgrade --install sample-app-secure ./sample-app --set image.tag=secure

# Output: Pod created, service is accessible.
```

---

### 3. Screenshots / Evidence

<img width="960" alt="Screenshot 2025-07-07 124409" src="https://github.com/user-attachments/assets/706b99f0-9f6d-43db-be7c-888c83eb60df" />

<img width="960" alt="Screenshot 2025-07-07 124232" src="https://github.com/user-attachments/assets/67197051-953d-4fdb-800d-8225821783ec" />

<img width="951" alt="Screenshot 2025-07-07 153028" src="https://github.com/user-attachments/assets/f74710a0-1e69-46b7-a13c-cd2f5f777e9e" />

---

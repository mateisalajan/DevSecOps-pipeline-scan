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
   ```bash
   git clone https://github.com/mateisalajan/DevSecOps-pipeline-scan.git
   cd DevSecOps-pipeline-scan
````

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

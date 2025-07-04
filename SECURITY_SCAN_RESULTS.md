# 🔒 Security Scan Results


This file tracks Trivy scan results for the app's Docker images.

---

## ❌ Initial Scan (Intentionally Vulnerable Image)

<details>
<summary>Show Trivy scan output (failing build)</summary>

```
sample-app:vuln (alpine 3.14.6)
Total: 16 vulnerabilities (HIGH: 15, CRITICAL: 1)

Top Findings:

* zlib (1.2.12-r0): CVE-2022-37434 — CRITICAL (heap-based buffer over-read)
* expat (2.4.7-r0): CVE-2022-40674, CVE-2022-43680 — HIGH
* openssl/libcrypto1.1: CVE-2023-0464 — HIGH
* flask (2.0.0): CVE-2023-30861 — HIGH
...
```

</details>

---

## ✅ Scan After Remediation (Fully Patched Image)

<details>
<summary>Show Trivy scan output (passing build, all issues resolved)</summary>

```
sample-app:secure (alpine 3.19.5)
Total: 0 vulnerabilities (HIGH: 0, CRITICAL: 0)

All system libraries and Python dependencies (Flask, Werkzeug, etc.): **CLEAN**
```

</details>

---

## 📊 Vulnerability Comparison Table

| Docker Image       | CRITICAL CVEs | HIGH CVEs | App Layer Vulnerabilities? |
| ------------------ | :-----------: | :-------: | :------------------------: |
| sample-app\:vuln   |       1       |     15    |             Yes            |
| sample-app\:secure |       0       |     0     |             No             |

---

### **Summary**

* The “vuln” image failed CI because of both CRITICAL and HIGH CVEs in system and app packages.
* After remediation, the “secure” image has **no vulnerabilities at all**—neither in system libraries nor application dependencies.
* This demonstrates full DevSecOps pipeline skills: detection, triage, and **complete remediation** of container security issues!

---

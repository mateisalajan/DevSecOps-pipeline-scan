# Security Scan Results

This file tracks the results of automated security scans using [Trivy](https://github.com/aquasecurity/trivy) in CI/CD.

---

## Initial Scan (Intentionally Vulnerable Image)

<details>
<summary>Show Trivy scan output (failing build)</summary>

sample-app:vuln (alpine 3.14.6)
===============================

Total: 16 vulnerabilities (HIGH: 15, CRITICAL: 1)

Top Findings:
- **zlib** (`1.2.12-r0`):  
  - [CVE-2022-37434](https://avd.aquasec.com/nvd/cve-2022-37434) — CRITICAL  
    Heap-based buffer over-read and overflow in inflate(), fixed in `1.2.12-r2`

- **expat** (`2.4.7-r0`):  
  - [CVE-2022-40674](https://avd.aquasec.com/nvd/cve-2022-40674) — HIGH  
    Use-after-free in doContent function, fixed in `2.4.9-r0`
  - [CVE-2022-43680](https://avd.aquasec.com/nvd/cve-2022-43680) — HIGH  
    Use-after free caused by overeager destruction of a shared DTD, fixed in `2.5.0-r0`

- **openssl/libcrypto1.1/libssl1.1**:  
  - [CVE-2023-0464](https://avd.aquasec.com/nvd/cve-2023-0464) — HIGH  
    Denial of service by excessive resource usage in verifying X509 policy, fixed in `1.1.1t-r1`

- **Flask (Python)** (`2.0.0`):  
  - [CVE-2023-30861](https://avd.aquasec.com/nvd/cve-2023-30861) — HIGH  
    Possible disclosure of permanent session cookie, fixed in `2.3.2`, `2.2.5`
	
</details>

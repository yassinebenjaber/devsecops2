# 🛡️ DevSecOps Werkstudent Interview Cheat Sheet 📘
## The Ultimate Revision for Yassine Ben Jaber (v6.0)

**Candidate:** Yassine Ben Jaber
**Focus:** DevSecOps (Shift-Left, Automation, Cloud/K8s Security)
**Goal:** Demonstrate applied knowledge, strategic thinking, and cultural fit during a 1-hour interview.

This README is a **concise, expert-level guide** with **internal navigation links**, focusing on applied security best practices, automation, and enforcement across the entire SDLC. **Enhanced visibility with keywords and emojis** for rapid reference.

---

## 🔹 Table of Contents

1. [Core DevSecOps Principles](#1️⃣-core-devsecops-principles)
    * [1.1 Shift-Left Security Philosophy ➡️](#11-shift-left-security-philosophy-➡️)
    * [1.2 Key Security Tools (SAST/DAST/SCA) 🛠️](#12-key-security-tools-sastdastsca-🛠️)

2. [CI/CD & Pipeline Security Gates ⚙️](#2️⃣-cicd--pipeline-security-gates-⚙️)
    * [2.1 The Security Gates Table 📊](#21-the-security-gates-table-📊)
    * [2.2 Secrets & Credential Management 🔑](#22-secrets--credential-management-🔑)

3. [Infrastructure as Code (IaC) Security 🏗️](#3️⃣-infrastructure-as-code-iac-security-🏗️)
    * [3.1 IaC Scans & Verification ✅](#31-iac-scans--verification-✅)
    * [3.2 Networking & IAM Best Practices 🔒](#32-networking--iam-best-practices-🔒)

4. [Containers & Kubernetes Security 🐳](#4️⃣-containers--kubernetes-security-🐳)
    * [4.1 Container Hardening & Runtime Config ⚙️](#41-container-hardening--runtime-config-⚙️)
    * [4.2 K8s Security: RBAC, Policies & Admissions 🛑](#42-k8s-security-rbac-policies--admissions-🛑)

5. [AWS Cloud Security Fundamentals ☁️](#5️⃣-aws-cloud-security-fundamentals-☁️)
    * [5.1 Shared Responsibility & IAM 🤝](#51-shared-responsibility--iam-🤝)
    * [5.2 Storage, Networking & Logging 💾](#52-storage-networking--logging-💾)

6. [Troubleshooting & Behavioral Tips 🧠](#6️⃣-troubleshooting--behavioral-tips-🧠)

---

## 1️⃣ Core DevSecOps Principles

| Concept | Description | Key Tools/Practices |
| :--- | :--- | :--- |
| **DevOps vs DevSecOps** | **DevOps:** Automates dev, test, deploy (speed). **DevSecOps:** Integrates **security at every stage** (secure speed). | `Build fast, deploy fast, but securely.` |
| **CI/CD** | **CI:** Merge code, automated builds & tests. **CD:** Deploy repeatably & safely. | Reduce errors, enforce quality & security. |
| **Pre-Commit Hooks** | **Prevent secrets/vulnerabilities** from entering Git **before** commit. | **git-secrets**, **trufflehog**, pre-commit framework. |
| **Vulnerability Workflow** | **Integrate** SAST/SCA/DAST. **Fail** builds for high-risk (CVSS ≥7.0). Track **MTTR** (Mean Time To Resolution). | Patch, update, re-scan. |

### 1.1 Shift-Left Security Philosophy ➡️
* **Integrate security early**: pre-commit hooks, SAST/SCA in local/CI pipelines.
* **Goal**: Block high-risk vulnerabilities immediately, making security **proactive**, not reactive.
* **Links:** [OWASP Top 10](https://owasp.org/Top10/)

### 1.2 Key Security Tools (SAST/DAST/SCA) 🛠️
| Tool Type | Analysis Type | Purpose | Example Tools |
| :--- | :--- | :--- | :--- |
| **SAST** | Static 📝 | Detect code vulnerabilities *without* running it. | **SonarQube**, **Semgrep** |
| **DAST** | Dynamic 🏃 | Simulate attacks on live endpoints (staging/test). | **OWASP ZAP** |
| **SCA** | Dependency 📦 | Check OSS dependencies for known CVEs. | **Snyk**, **Dependency-Check** |

---

## 2️⃣ CI/CD & Pipeline Security Gates ⚙️

### 2.1 The Security Gates Table 📊
A well-secured pipeline has automated checks at every transition point.

| Stage | Action / Check | Tool Example |
| :--- | :--- | :--- |
| 📝 **Code** | Block secrets/high-entropy strings. | **trufflehog** (pre-commit) |
| 🏗️ **Build** | SAST/SCA scan code/dependencies. | **SonarQube**, **Snyk** |
| ⚙️ **IaC** | Validate config against best practices (CIS). | **Checkov**, **Terrascan** |
| 🧪 **Test/Staging** | DAST scan on running application endpoints. | **OWASP ZAP** |
| 🐳 **Artifact** | Container image vulnerability scan. | **Trivy**, **Clair** |
| 🚀 **Deploy** | Enforce K8s/Cloud Admission Controls. | **Gatekeeper** (K8s), Policy-as-Code. |

### 2.2 Secrets & Credential Management 🔑
* **Jenkins Best Practice:** Use **least-privilege service accounts** and inject secrets via the **credentials API**, *not* environment variables.
* **Anti-Pattern:** Never **hardcode** tokens or API keys in code or IaC.
* **Solution:** Inject secrets at runtime using dedicated managers: **AWS Secrets Manager**, **Vault**, or **K8s Secrets** (if encrypted).
* **Links:** [Jenkins Security](https://www.jenkins.io/doc/book/security/)

---

## 3️⃣ Infrastructure as Code (IaC) Security 🏗️

### 3.1 IaC Scans & Verification ✅
* Validate IaC (e.g., Terraform) against **CIS benchmarks** and **Security Policy as Code**.
* Tools like **Checkov** or **Terrascan** find misconfigurations like public S3 buckets or overly permissive IAM policies **pre-deployment**.
* **Gate:** Fail builds on high-risk misconfigurations (e.g., unencrypted S3, public DBs).

### 3.2 Networking & IAM Best Practices 🔒
* **Networking:** Configure SGs/NACLs with **least privilege**. **AVOID** `0.0.0.0/0` inbound access. Limit to trusted IPs/VPCs.
* **IAM:** Enforce **Policy-as-Code** (e.g., in Terraform) to prevent over-permissive defaults. Use **roles** instead of long-lived access keys.

---

## 4️⃣ Containers & Kubernetes Security 🐳

### 4.1 Container Hardening & Runtime Config ⚙️
| Concept | Security Action | Command Example |
| :--- | :--- | :--- |
| **Base Image** | Use **minimal base images** (Alpine, Scratch). | `FROM alpine:3.18` |
| **Users** | Run containers as a **non-root user**. | `USER appuser` |
| **Hardening** | Use multi-stage builds. Set read-only filesystems. | `RUN chown -R appuser:appuser /app` |
| **Scanning** | Scan pre-deployment and enforce policy. | **Trivy**, **Clair** |

### 4.2 K8s Security: RBAC, Policies & Admissions 🛑
* **RBAC (Role-Based Access Control):** Restrict pod-to-pod permissions and administrator access. Principle of **Least Privilege**.
* **NetworkPolicies:** Restrict pod-to-pod communication (**micro-segmentation**). Use isolated **namespaces** for multi-tenancy.
* **Secrets:** Use **Vault** or **K8s Secrets** (with encryption enabled) and avoid embedding them in manifests/images.
* **Admission Controls:** Enforce image scanning/security policies **before** a pod is deployed to the cluster.
* **Runtime:** Use **Falco** for runtime anomaly detection and syscall monitoring.
* **Links:** [Kubernetes Security Documentation](https://kubernetes.io/docs/concepts/security/)

---

## 5️⃣ AWS Cloud Security Fundamentals ☁️

### 5.1 Shared Responsibility & IAM 🤝
* **Shared Responsibility Model:** **AWS** is responsible for the **infrastructure** (Security *of* the Cloud). **You** are responsible for **everything else** (Security *in* the Cloud: IAM, apps, configs, data).
    * **Link:** [AWS Shared Responsibility Model](https://aws.amazon.com/compliance/shared-responsibility-model/)
* **IAM Best Practices:** **MFA** for all users, use **least-privilege roles**, use **temporary credentials** (assume role), rotate keys regularly.

### 5.2 Storage, Networking & Logging 💾
* **Storage (S3/EBS):** **Private** S3 buckets by default. Enforce **SSE-KMS encryption**. Enable **MFA Delete** and **versioning**.
* **Networking:**
    * **Security Groups (SGs):** **Instance-level**, **stateful** firewall.
    * **NACLs (Network Access Control Lists):** **Subnet-level**, **stateless** firewall.
* **Monitoring & Logging:**
    * **CloudTrail:** **API activity logs** (Who did what, when).
    * **GuardDuty:** **Threat detection** and anomaly alerts.
    * **CloudWatch:** Metrics, alarms, central log aggregation.

---

## 6️⃣ Troubleshooting & Behavioral Tips 🧠

| Topic | Key Action/Mindset | Communication Focus |
| :--- | :--- | :--- |
| **Troubleshooting** | **Structured Approach:** **Logs first** $\rightarrow$ Check **IAM** $\rightarrow$ Check **SGs/NACLs/NetworkPolicies** $\rightarrow$ **Firewall** rules. | *"If I'm unsure, I check logs, IAM, SGs, and then firewall rules."* |
| **Communication** | **Developers:** Focus on **tools & configurations** (`"RBAC ensures pods access only necessary resources."`). | **Managers:** Focus on **risk & compliance** (`"Automated SCA reduces legal/financial exposure from vulnerable OSS code."`). |
| **Speed vs Security** | Security is a **gate**, not a hurdle. Automate SAST/SCA and focus on prioritizing **top threats** (CVSS >7.0). | *"We achieve both by automating security tests and failing the build early."* |
| **KPIs (Key Metrics)** | **Deployment Frequency** $\uparrow$, **MTTR** (Mean Time To Resolution) $\downarrow$, **% Automated Security Tests** $\uparrow$, **Critical Findings** $\downarrow$. | *Focus on measurability and continuous improvement.* |
| **Linux Security** | **Identify open ports:** `netstat -tulnp` or `ss -tulnp`. **Manage permissions:** `chmod`, `chown`. Ensure firewall (iptables/UFW) matches architecture. | **Links:** [Linux Security Basics](https://linuxsecurity.expert/) |

---

**Good luck, Yassine! You've got this. 🚀**

> Hands-on DevSecOps experience + automation mindset + security-first thinking = strong, fast-access interview prep.

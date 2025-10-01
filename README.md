## 🛡️ DevSecOps Werkstudent Interview Master Sheet 📘

## 🎤 Interview Introduction & Experience Script

### Introduction & Focus (The Hook)

"Hello! Thanks for taking the time to meet with me today, Mr. Scherzer. I'm currently wrapping up my Computer Science engineering degree and pursuing my Masters at the University of Marburg.

My focus has largely been on **Network Infrastructure and Data Security**, which includes relevant studies in **DevSecOps, Cloud security, and Virtualization.**

Honestly, my favorite area, and where I aim to contribute most, is **Security Automation** within the CI/CD pipeline, and building **Secure Cloud/Container Architectures**. That's why this DevSecOps role, focusing on tooling and workflow optimization, is exactly what I'm looking for."

### Professional Experience Summary

**1. Foundational Skills (STEG)**

"My first internship was at the Tunisian Electricity and Gas Company. It was my first exposure to a professional IT environment. I gained basic IT security and operational skills, like checking firewall configurations and evaluating system setups. It really taught me the importance of **structure and clear documentation** in any engineering setting."

**2. DevSecOps Implementation & AWS (Linedata) - (The Core Match)**

"My second internship at Linedata gave me hands-on DevSecOps experience that directly relates to your team's work:
* **The Project:** I helped the cloud team migrate our CI/CD process from a costly proprietary tool, Harness.io, to a custom, open-source **Jenkins pipeline**.
* **Automation:** I built the foundational infrastructure using **Terraform** for **EC2 VM provisioning** and **Ansible** for **configuration management**, ensuring the entire build environment was reproducible—which is key for documentation.
* **AWS Security:** We secured the Jenkins **EC2 instance** rigorously. This involved setting a strict **Security Group** for network access and securing access to **S3 artifact storage** using a **least-privilege IAM role** and **Bucket Policies**.
* **Pipeline Security:** I integrated **pre-commit hooks** for early checks, ran **SonarQube** for code quality, and used **OWASP ZAP** for dynamic application scanning.
* **Takeaway:** This project cemented my skills in **IaC, Jenkins, and practical AWS security**, leading me to earn my **AWS Certified Cloud Practitioner** certification."

**3. Applied Cybersecurity & Automation (ANCS-tunCERT)**

"My third internship was focused on the Blue Team side, working at the Tunisian Cybersecurity Agency.
* **The Project:** I prototyped a **Machine Learning model using Python** and Scikit-learn to help reduce false positives coming from our SIEM, **Wazuh**.
* **Process Focus:** Although the ML project was a prototype and wasn't fully productionized, I gained crucial experience in **structured data analysis and preprocessing**. I learned to effectively **balance precision vs. recall**, which is a vital skill for optimizing *any* security tool in a fast-paced environment.
* **Certifications:** I also leveraged this time to certify my knowledge with the **ISC² Certified in Cybersecurity** and the **ISO 27001 Associate certificate**."

**4. Advanced Automation & Documentation (BMW Group)**

"My most recent internship at BMW focused on fuzzy testing on their newest infotainment, where **Python automation** was crucial.
* **The Work:** I developed toolkits for protocol **fuzzing** on the infotainment system (Targeting connectivity interfaces: WLAN, USB and Bluetooth), including complex techniques like **adaptive mutationa for frame injection and Bluetooth L2CAP Packets**.
* **DevOps Relevance:** The biggest takeaway for me was the need for **reproducibility**. I spent significant effort **automating** these tests and creating clear, usable **documentation on Confluence and GitHub**, directly linking my findings to scalable, documented workflows—a skill highly relevant to this role."

---

## Portfolio Projects (The Scripts)

### 1. Foundational DevSecOps Pipeline (Jenkins/Vagrant)
<a name="71-foundational-pipeline-detailed-script"></a>
> "This is a school project where I built a full DevSecOps pipeline using **Vagrant and Jenkins**. **Vagrant** provisions a reproducible environment for the pipeline. **Jenkins** pulls the code from GitHub, where we also run **pre-commit checks**. The code is built with **Maven** and unit tested using **Mockito**. Security and quality gates are enforced with **OWASP Dependency Check** and **SonarQube**. Artifacts are stored in **Nexus**, Docker images are built, old containers cleaned up, and services deployed via **Docker Compose**. We verify open ports with **Nmap** and perform **OWASP TAP Baseline checks**. Finally, **Grafana and Prometheus** monitor the services, covering the full flow in a controlled, repeatable environment."

### 2. Modern GitOps Pipeline (GitHub Actions/ArgoCD)
<a name="72-modern-gitops-pipeline-detailed-script"></a>
> "For a cloud-native project, whenever a developer creates a commit or a pull request, we have **GitHub Workflows** configured. This CI runs multiple jobs (unit testing, SAST, build, docker). The **docker job** includes **scanning the image using Trivy** before uploading it to **GitHub Container Registry**. Once CI is done, we use **ArgoCD** for CD, where it **continuously detects changes** in the **Helm chart** and pulls the latest image stack to deploy to the **Kubernetes cluster**. This is a typical end-to-end GitOps pipeline."

---

### 🔹 Table of Contents

1. [Core Principles & Tooling (Job Match)](#1-core-principles-tooling) 🛠️
    * [1.1 Shift-Left Security Philosophy](#11-shift-left-security-philosophy) ➡️
    * [1.2 Key Security Tools (SAST/DAST/SCA)](#12-key-security-tools) 🔎

2. [CI/CD & Jenkins Automation](#2-cicd-jenkins-automation) ⚙️
    * [2.1 Jenkins Pipeline Security Gates](#21-jenkins-pipeline-security-gates) 📊
    * [2.2 Secrets & Credential Management](#22-secrets-credential-management) 🔑

3. [Infrastructure as Code (IaC) & Provisioning](#3-iac-provisioning) 🏗️
    * [3.1 IaC Scans & Best Practices](#31-iac-scans-best-practices) ✅
    * [3.2 VM Provisioning (Automation Focus)](#32-vm-provisioning) 🖥️

4. [Containers & Kubernetes Security](#4-containers-kubernetes-security) 🐳
    * [4.1 Container Hardening & Runtime Config](#41-container-hardening) ⚙️
    * [4.2 K8s Security: RBAC, Policies & Admissions](#42-k8s-security) 🛑

5. [AWS Cloud Security & Architecture (Matthias Match)](#5-aws-cloud-security) ☁️
    * [5.1 Shared Responsibility & IAM](#51-shared-responsibility-iam) 🤝
    * [5.2 Storage, Networking & Logging](#52-storage-networking-logging) 💾

6. [Communication & Behavioral Tips (Training/Documentation)](#6-communication-behavioral-tips) 🧠

7. [Project Experience Examples (STAR Format)](#7-project-experience-examples) 🛠️

8. [Deep Dive Technical Concepts (Gotchas)](#8-deep-dive-technical-concepts) 💡

---
<br>

## 1. Core Principles & Tooling (Job Match) 🛠️
<a name="1-core-principles-tooling"></a>

| Concept | Description | Key Tools/Practices |
| :--- | :--- | :--- |
| **DevOps vs DevSecOps** | **DevOps:** Automates dev, test, deploy (speed). **DevSecOps:** Integrates **security at every stage** (secure speed, risk reduction). | Security is a **gate**, not a hurdle. |
| **Tool Implementation** | Process of integrating a security tool (SAST/SCA/DAST) into the **CI/CD pipeline** and configuring rules to **fail the build** on critical findings. | Jenkins pipeline steps (e.g., `sh 'trivy...'`). |
| **Documentation Focus** | Creating clear, understandable guides (e.g., Confluence, Readme files) for developers/users on **how to use the automated tools** and **how to resolve findings**. | Focus on **process optimization** (workflow, MTTR). |

### 1.1 Shift-Left Security Philosophy ➡️
<a name="11-shift-left-security-philosophy"></a>
* **Definition:** Integrating security practices **as early as possible** in the SDLC (e.g., pre-commit hooks, local SAST scans).
* **Goal:** Catch vulnerabilities when they are **easiest and cheapest to fix** (developer desktop vs. production).
* **Links:** [OWASP Top 10](https://owasp.org/Top10/)

### 1.2 Key Security Tools (SAST/DAST/SCA) 🔎
<a name="12-key-security-tools"></a>
| Tool Type | Analysis Type | Purpose | Example Tools (Experience) |
| :--- | :--- | :--- | :--- |
| **SAST** | Static 📝 | Detect code vulnerabilities *without* running it. (**Code Quality**) | **SonarQube** (Used at Linedata), **Semgrep** |
| **DAST** | Dynamic 🏃 | Simulate attacks on live endpoints (staging/test). (**Runtime Security**) | **OWASP ZAP** (Used at Linedata) |
| **SCA** | Dependency 📦 | Check OSS dependencies for known CVEs. (**Vulnerability Management**) | **Snyk**, **Dependency-Check** |

---
<br>

## 2. CI/CD & Jenkins Automation ⚙️
<a name="2-cicd-jenkins-automation"></a>

### 2.1 Jenkins Pipeline Security Gates 📊
<a name="21-jenkins-pipeline-security-gates"></a>
A well-secured pipeline has automated checks at every transition point. (My experience includes using **Jenkins with AWS/SonarQube/ZAP**.)

| Stage | Action / Check | Tool Example (My Experience) |
| :--- | :--- | :--- |
| 📝 **Code** | Block secrets/high-entropy strings. | **trufflehog** (pre-commit hook) |
| 🏗️ **Build** | SAST/SCA scan code/dependencies. **Fail build** for severity $\ge$ 7.0. | **SonarQube**, **Snyk** |
| ⚙️ **IaC** | Validate config against secure benchmarks. | **Checkov**, **Terrascan** |
| 🧪 **Test/Staging** | DAST scan on running application endpoints. | **OWASP ZAP** Baseline Scan |
| 🐳 **Artifact** | Container image vulnerability scan. | **Trivy**, **Clair** |
| 🚀 **Deploy** | Enforce security policies via Admission Controls. | **Gatekeeper** (K8s) |

### 2.2 Secrets & Credential Management 🔑
<a name="22-secrets-credential-management"></a>
* **Jenkins Implementation:** Use **Jenkins Credentials API** to inject secrets into the pipeline, and ensure the pipeline uses **least-privilege service accounts**.
* **Anti-Pattern:** Never **hardcode** tokens/keys in code or IaC.
* **Solution:** Use runtime injection: **AWS Secrets Manager** (relevant to Matthias/AWS focus) or a dedicated Vault.

---
<br>

## 3. Infrastructure as Code (IaC) & Provisioning 🏗️
<a name="3-iac-provisioning"></a>

### 3.1 IaC Scans & Best Practices ✅
<a name="31-iac-scans-best-practices"></a>
* **Purpose:** Validate IaC (e.g., Terraform) against **CIS benchmarks** and prevent misconfigurations **pre-deployment**.
* **Implementation:** Tools like **Checkov** or **Terrascan** check for public S3 buckets, overly permissive IAM, and missing encryption.
* **Gate:** IaC scans are a crucial **Shift-Left** gate for infrastructure security.

### 3.2 VM Provisioning (Automation Focus) 🖥️
<a name="32-vm-provisioning"></a>
* **Job Requirement Match:** The requirement to assist with **VM provisioning automation** points to tools like **Ansible, Terraform, or Packer**.
* **My Experience Match:** My experience with **Terraform (IaC)** and **Ansible (SOAR/Automation)** allows for securing this process.
* **Security Checkpoints:** Provisioning must ensure **minimum OS hardening** (e.g., non-root users, firewalls enabled), **least privilege IAM roles**, and **encrypted volumes**.

---
<br>

## 4. Containers & Kubernetes Security 🐳
<a name="4-containers-kubernetes-security"></a>

### 4.1 Container Hardening & Runtime Config ⚙️
<a name="41-container-hardening"></a>
| Concept | Security Action | Justification |
| :--- | :--- | :--- |
| **Base Image** | Use **minimal base images** (Alpine, Scratch). | Reduces attack surface by eliminating unnecessary packages. |
| **Users** | Run containers as a **non-root user**. | Prevents host compromise if the container breaks out. |
| **Scanning** | Scan images (Trivy, Clair) **before** pushing to the registry. | Ensures only validated, low-risk artifacts are available for deployment. |
| **Multi-Stage Builds** | Separate build dependencies from the final runtime image. | Limits the secrets and tools available in the production environment. |

### 4.2 K8s Security: RBAC, Policies & Admissions 🛑
<a name="42-k8s-security"></a>
* **RBAC (Role-Based Access Control):** Restrict who (user/pod) can do what in the cluster. **Principle of Least Privilege.**
* **Admission Controls:** Enforce security policies **before** a pod is deployed. (e.g., preventing containers running as root).
* **Runtime:** Use **Falco** or similar tools for real-time anomaly detection based on syscalls.

---
<br>

## 5. AWS Cloud Security & Architecture (Matthias Match) ☁️
<a name="5-aws-cloud-security"></a>

### 5.1 Shared Responsibility & IAM 🤝
<a name="51-shared-responsibility-iam"></a>
* **Shared Responsibility Model:** AWS secures the **infrastructure** (Security *of* the Cloud). **We** secure **IAM, applications, and configurations** (Security *in* the Cloud).
* **IAM Architecture:** Use **Roles** for temporary, least-privilege access for applications (EC2/Lambda), not long-lived keys. Enforce **MFA** for all users.

### 5.2 Storage, Networking & Logging 💾
<a name="52-storage-networking-logging"></a>
* **Storage (S3):** All buckets **Private** by default. Enforce **SSE-KMS encryption**. Use **Bucket Policies** to enforce secure access.
* **Networking:**
    * **Security Groups (SGs):** **Stateful** (Outbound traffic is automatically allowed back in).
    * **NACLs (Network Access Control Lists):** **Stateless** (Must allow traffic in **and** out explicitly).
* **Monitoring & Logging:**
    * **CloudTrail:** **API activity logs** (Who did what, when - **Audit/Compliance**).
    * **GuardDuty:** **Threat detection** (ML-powered anomaly alerts).

---
<br>

## 6. Communication & Behavioral Tips (Training/Documentation) 🧠
<a name="6-communication-behavioral-tips"></a>

| Topic | Key Action/Mindset | Job Requirement Focus |
| :--- | :--- | :--- |
| **Documentation** | **Focus on the audience.** Document the **"Why"** (risk) and the **"How-To"** (resolution). Use Confluence/GitHub for clarity and accessibility. | *“I use detailed documentation (like the reports I made for BMW/Confluence) to create clear **training materials** for developers.”* |
| **Communication** | **Developers:** Focus on **tools & configuration** and provide specific fixes. **Managers:** Focus on **risk, compliance, and MTTR.** | *“I enjoy preparing and communicating complex technical content in an understandable way (Job Profile Match).”* |
| **Troubleshooting** | **Structured Approach:** **Logs first** $\rightarrow$ Check **IAM** $\rightarrow$ Check **SGs/NACLs/NetworkPolicies** $\rightarrow$ **Firewall** rules. | *“I always use a structured, independent approach to solve technical problems, starting with log analysis (Wazuh/ELK/Splunk experience).”* |
| **My Experience Summary (STAR)** | **DevSecOps Linedata:** CI/CD with **AWS (EC2/S3), Jenkins, SonarQube, OWASP ZAP**. Proactively implemented **Pre-Commit-Hooks**. | Emphasizes **DevSecOps/CI/CD** experience required by the job. |

---
<br>

## 7. Project Experience Examples (STAR Format) 🛠️
<a name="7-project-experience-examples"></a>

| Project Focus | 1. Foundational DevSecOps Pipeline (Jenkins/Vagrant) | 2. Cloud-Native GitOps Pipeline (GitHub Actions/ArgoCD) |
| :--- | :--- | :--- |
| **CI Orchestration** | **Jenkins** running on a consistent, reproducible **Vagrant VM**. | **GitHub Workflows** (Unit Test, SAST, Build, Docker, Stack Update jobs). |
| **Key Tools/Steps** | **Pre-commit** checks $\rightarrow$ **Maven** build/Mockito test $\rightarrow$ **OWASP Dependency Check** (SCA) & **SonarQube** (SAST) gates. | **Trivy** (Scanning) integrated directly into the Docker job $\rightarrow$ Artifacts pushed to **GitHub Container Registry**. |
| **Artifact & Deployment** | Artifacts stored in **Nexus**. Deployment via **Docker Compose**. Open ports verified with **Nmap**. | **ArgoCD** for Continuous Deployment (CD). It continuously monitors the **Helm Chart** repository (GitOps). |
| **Monitoring & Verification** | **OWASP TAP Baseline** checks for production readiness. **Prometheus & Grafana** for monitoring. | ArgoCD pulls the latest image stack and deploys to the **Kubernetes cluster**. |
| **Result/Value** | Created a **fully controlled, repeatable, and documented blueprint** for a secure SDLC in a simulated environment. | Achieved **declarative, fast, and auditable deployment** through a modern, cloud-native GitOps workflow. |

---
<br>

## 8. Deep Dive Technical Concepts (Gotchas) 💡
<a name="8-deep-dive-technical-concepts"></a>

| Topic | The Concept | Technical Depth / Distinction |
| :--- | :--- | :--- |
| **Jenkins: `stage` vs `script`** | **Context:** Declarative Pipeline. | A **`stage`** is for **visualization** (Build, Test, Deploy). The **`script`** block is an **'escape hatch'** to use raw Groovy for complex logic (variables, loops, try/catch) inside a stage's `steps` section. |
| **Docker: CMD vs ENTRYPOINT** | **Context:** Defining container runtime. | **`CMD`** sets the **default command** which can be overridden (e.g., `bash`). **`ENTRYPOINT`** sets the **main executable** and is rarely overridden (e.g., `java -jar`). They often work together. |
| **IaC: Idempotency** | **Context:** Terraform/Ansible. | The property that a deployment run will always yield the **same result**, regardless of how many times it is executed. It prevents unintended changes or resource duplication. |
| **K8s: ServiceAccount Token** | **Context:** Pod Identity. | A **ServiceAccount** provides an **identity** to a pod. The token allows the pod to authenticate and communicate with the **Kubernetes API Server** (e.g., read secrets, create new pods). |
| **AWS: SG vs NACL (Recap)** | **Context:** Network Security. | **SG** is **Stateful** (allows return traffic automatically), applies to **EC2/ENI**. **NACL** is **Stateless** (must define in and out rules), applies to **Subnets**. |

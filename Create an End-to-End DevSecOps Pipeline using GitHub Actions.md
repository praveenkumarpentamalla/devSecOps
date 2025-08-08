# 📌 Assignment Title: Create an End-to-End DevSecOps Pipeline using GitHub Actions for a C# Application

---

## 📄 Description

In this task, you are required to create a **DevSecOps pipeline** with the following stages using **GitHub Actions**:

### ✅ Stage 1: SonarCloud Analysis  
Run **SonarCloud** analysis on the C# source code to assess code quality and identify bugs, vulnerabilities, and code smells.

### ✅ Stage 2: Software Composition Analysis (SCA)  
Use **Snyk** to perform **SCA** and detect vulnerabilities in open-source dependencies.

### ✅ Stage 3: Dynamic Application Security Testing (DAST)  
Run a **DAST scan** targeting the URL: [http://example.com](http://example.com) to identify runtime vulnerabilities.

---

## 🔗 C# Sample Application Repository

Use the following GitHub repository containing a sample C# application to implement the end-to-end DevSecOps pipeline:

👉 [Assignment Repository - C# App for DevSecOps](https://github.com/asecurityguru/devsecops-dotnet-github-actions-end-to-end-assignment)

---

## 🧪 Reference Solution (For Review After Implementation Only)

Once you've completed your own GitHub Actions workflow, you can refer to the solution repository below.  
It contains the workflow file **`devsecops-workflow.yaml`** which includes all required stages: **SAST**, **SCA**, and **DAST**.

👉 [Solution Repository - Completed DevSecOps Workflow](https://github.com/asecurityguru/devsecops-dotnet-github-actions-end-to-end-solution)

---
# 🛠️ Facing Errors While Running DAST Scan Using GitHub Actions?

If you're encountering the following error while running a **DAST (Dynamic Application Security Testing)** scan using GitHub Actions:

![DAST Scan Error](https://img-c.udemycdn.com/redactor/raw/article_lecture/2023-01-10_07-17-09-775d14acaf9056fc13d86cda933b5dc6.png)

---

## ✅ Solution

### ✔️ Check Branch Name in GitHub Actions Workflow

Ensure that your **branch name** in the GitHub Actions workflow file for **OWASP ZAP** is **correct**.

For example, in the screenshot below, the **highlighted branch name** should match **exactly** with the branch from which you're triggering the workflow. If there's a mismatch, the DAST scan will fail.

![Branch Name Configuration](https://img-c.udemycdn.com/redactor/raw/article_lecture/2023-01-10_07-12-53-fec7b685b9c5faad20dcdd1ea6538259.png)

---

### ⚠️ Important Note

- **Do NOT** run the DAST scan on a **cloned repository**.
- Always run the DAST scan from a **fresh/original repository**.

---

# **Application Security Testing: Concepts and Tools**  
*Notebook Based on the Lecture Transcript*  

---

## **Table of Contents**  
1. [Introduction](#introduction)  
2. [Static Application Security Testing (SAST)](#sast)  
3. [Software Composition Analysis (SCA)](#sca)  
4. [Dynamic Application Security Testing (DAST)](#dast)  
5. [Interactive Application Security Testing (IAST)](#iast)  
6. [Infrastructure as Code (IaC) Security](#iac)  
7. [API and Microservice Security](#api)  
8. [Conclusion](#conclusion)  

---

## **1. Introduction** <a name="introduction"></a>  
Application security is a critical aspect of software development that ensures protection against vulnerabilities and threats. This notebook covers key security testing methodologies used in modern software development.  

---

## **2. Static Application Security Testing (SAST)** <a name="sast"></a>  

### **Definition**  
SAST (**Static Application Security Testing**) is a **white-box testing** method that analyzes **source code** to identify security vulnerabilities before the application is executed.  

### **Key Features**  
- Performed **without executing** the application.  
- Helps detect issues like **SQL injection, buffer overflows, and insecure coding practices**.  
- Can be done **manually** (code reviews) or **automated** (using specialized tools).  

### **Tools for SAST**  
| Tool | Description |  
|------|------------|  
| **Fortify** | Scans source code for vulnerabilities and provides remediation guidance. |  
| **Veracode** | Offers static analysis for identifying security flaws in applications. |  
| **SonarQube** | Open-source tool for continuous inspection of code quality and security. |  

### **Example**  
```java
// Vulnerable Code (SQL Injection)  
String query = "SELECT * FROM users WHERE username = '" + userInput + "'";  
```  
🔹 **SAST Tool Detection**: Flags this as a security risk due to possible SQL injection.  

### **Visualization**  
![SAST Process](https://www.example.com/sast-flow.png) *(Example: SAST scanning source code for flaws)*  

---

## **3. Software Composition Analysis (SCA)** <a name="sca"></a>  

### **Definition**  
SCA (**Software Composition Analysis**) identifies **third-party libraries** used in an application, checks for **security vulnerabilities**, and ensures **license compliance**.  

### **Why is SCA Important?**  
- Many applications use **open-source libraries** with known vulnerabilities.  
- Ensures legal compliance with software licenses (e.g., **GPL, MIT, Apache**).  

### **Tools for SCA**  
| Tool | Description |  
|------|------------|  
| **Snyk** | Scans dependencies for vulnerabilities and suggests fixes. |  
| **OWASP Dependency-Check** | Detects vulnerable libraries in Java, .NET, and more. |  

### **Example**  
🔹 **Scenario**: A project uses **Log4j 2.14.1** (affected by **CVE-2021-44228**).  
🔹 **SCA Tool Detection**: Alerts about the vulnerability and suggests upgrading to a secure version.  

---

## **4. Dynamic Application Security Testing (DAST)** <a name="dast"></a>  

### **Definition**  
DAST (**Dynamic Application Security Testing**) is a **black-box testing** method that scans **running applications** (web/mobile) for vulnerabilities.  

### **Key Features**  
- Tests applications **from an attacker’s perspective**.  
- Detects runtime issues like **XSS, CSRF, and authentication flaws**.  

### **Tools for DAST**  
| Tool | Description |  
|------|------------|  
| **Burp Suite** | Popular for manual and automated web security testing. |  
| **OWASP ZAP** | Free and open-source DAST tool for finding vulnerabilities. |  
| **Veracode DAST** | Automated scanning for web applications. |  

### **Example**  
🔹 **Test Case**: Sending a malicious payload (`<script>alert(1)</script>`) to a login form.  
🔹 **DAST Detection**: Identifies if the application is vulnerable to **Cross-Site Scripting (XSS)**.  

---

## **5. Interactive Application Security Testing (IAST)** <a name="iast"></a>  

### **Definition**  
IAST (**Interactive Application Security Testing**) combines **SAST + DAST** by analyzing code **while the application is running**.  

### **Advantages Over SAST & DAST**  
- Reduces **false positives** by validating findings in real-time.  
- Works well in **CI/CD pipelines**.  

### **Example**  
🔹 **Scenario**: Detects a **SQL injection** while the application processes user input.  
🔹 **IAST Action**: Logs the issue with exact code location and attack vector.  

---

## **6. Infrastructure as Code (IaC) Security** <a name="iac"></a>  

### **Definition**  
IaC (**Infrastructure as Code**) uses **code files** (e.g., Terraform, CloudFormation) to **automate infrastructure deployment**.  

### **Security Risks in IaC**  
- Misconfigured cloud storage (**public S3 buckets**).  
- Overprivileged IAM roles.  

### **Tools for IaC Security**  
| Tool | Description |  
|------|------------|  
| **Terraform Scan** | Checks for security misconfigurations in `.tf` files. |  
| **AWS CloudFormation Guard** | Validates templates against security rules. |  

### **Example**  
```yaml
# Insecure CloudFormation S3 Bucket  
Resources:  
  MyBucket:  
    Type: AWS::S3::Bucket  
    Properties:  
      AccessControl: PublicRead  # 🚨 Security Risk!  
```  
🔹 **IaC Security Tool Detection**: Flags this as a **publicly accessible bucket risk**.  

---

## **7. API and Microservice Security** <a name="api"></a>  

### **Definition**  
- **API Security**: Protects APIs from attacks like **injection, broken authentication, and data exposure**.  
- **Microservices**: Smaller, independent services within an API (e.g., **User Registration Service**).  

### **Example**  
🔹 **E-Commerce API** has:  
- `/users/create` (Microservice)  
- `/users/delete` (Microservice)  
🔹 **Security Testing**: Checks for **JWT validation, rate limiting, and input sanitization**.  

### **Tools**  
- **Postman** (API testing)  
- **OWASP API Security Top 10** (Guidelines)  

---

## **8. Conclusion** <a name="conclusion"></a>  
- **SAST** → Static code analysis.  
- **DAST** → Dynamic testing of running apps.  
- **IAST** → Hybrid approach.  
- **SCA** → Third-party library checks.  
- **IaC Security** → Secure cloud deployments.  
- **API Security** → Protect APIs and microservices.  

By integrating these security practices, developers can build **more secure applications**.  

---

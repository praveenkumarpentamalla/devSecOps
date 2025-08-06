# **GitHub Actions: Comprehensive Guide**

## **1. Introduction to GitHub Actions**
GitHub Actions is a **CI/CD (Continuous Integration and Continuous Delivery) platform** that allows you to automate workflows directly within GitHub.  

### **Key Uses of GitHub Actions**  
- **Automate Builds & Tests**: Run tests automatically when code is pushed.  
- **Deploy Applications**: Automate deployments to cloud platforms (AWS, Azure, GCP).  
- **Security Scanning**: Integrate SAST, DAST, and SCA tools (SonarQube, Snyk, OWASP ZAP).  
- **Scheduled Tasks**: Run jobs at specific times (e.g., nightly security scans).  

---

## **2. Core Components of GitHub Actions**
| Component | Description | Example |
|-----------|-------------|---------|
| **Workflows** | YAML files defining automation steps. | `.github/workflows/build.yml` |
| **Events** | Triggers that start workflows (push, PR, schedule). | `on: push` |
| **Jobs** | Group of steps running on the same runner. | `jobs: build: ...` |
| **Steps** | Individual tasks in a job (commands or actions). | `- run: npm install` |
| **Actions** | Reusable code from GitHub Marketplace. | `actions/checkout@v3` |
| **Runners** | Machines (Ubuntu, Windows, macOS) that execute jobs. | `runs-on: ubuntu-latest` |

---

## **3. GitHub Actions YAML Keywords Explained**
### **1. `name`**
- **Purpose**: Identifies the workflow in GitHub’s UI.  
- **Example**:
  ```yaml
  name: Security Pipeline
  ```

### **2. `on`**
- **Purpose**: Defines **trigger events** for the workflow.  
- **Common Events**:
  - `push`: Runs on new commits.  
  - `pull_request`: Runs on PR creation/update.  
  - `schedule`: Cron-based triggers (e.g., `0 2 * * *` for 2 AM daily).  
- **Example**:
  ```yaml
  on:
    push:
      branches: [ main ]
    pull_request:
      branches: [ main ]
  ```

### **3. `jobs`**
- **Purpose**: Groups **one or more jobs** that run in parallel or sequentially.  
- **Example**:
  ```yaml
  jobs:
    build:
      runs-on: ubuntu-latest
      steps: [...]
  ```

### **4. `runs-on`**
- **Purpose**: Specifies the **OS environment** (runner) for the job.  
- **Options**: `ubuntu-latest`, `windows-latest`, `macos-latest`.  
- **Example**:
  ```yaml
  jobs:
    test:
      runs-on: ubuntu-latest
  ```

### **5. `steps`**
- **Purpose**: Contains **individual tasks** in a job.  
- **Key Sub-Keywords**:
  - `uses`: Reuses an action (e.g., `actions/checkout@v3`).  
  - `run`: Executes shell commands.  
  - `name`: Labels the step in logs.  
- **Example**:
  ```yaml
  steps:
    - name: Checkout code
      uses: actions/checkout@v3
    - name: Run tests
      run: npm test
  ```

### **6. `env`**
- **Purpose**: Sets **environment variables** for the workflow.  
- **Example**:
  ```yaml
  env:
    NODE_ENV: production
  ```

### **7. `strategy`**
- **Purpose**: Defines **matrix builds** (e.g., testing across multiple OS/versions).  
- **Example**:
  ```yaml
  strategy:
    matrix:
      os: [ubuntu-latest, windows-latest]
      node: [14, 16]
  ```

### **8. `if`**
- **Purpose**: Adds **conditional logic** to steps/jobs.  
- **Example**:
  ```yaml
  steps:
    - name: Notify Slack
      if: failure()
      run: ./notify-slack.sh
  ```

---

## **4. Example Workflow Breakdown**
```yaml
name: Security Scan Pipeline

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  security-checks:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      
      - name: Run SAST with SonarQube
        uses: SonarSource/sonarcloud-github-action@master
        env:
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
      
      - name: Dependency Scan with Snyk
        uses: snyk/actions/node@master
        env:
          SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
```

---

## **5. Key Notes from the Transcript**
1. **Workflow Files**: Stored in `.github/workflows/` (e.g., `build.yml`).  
2. **Event Triggers**:  
   - `push` → Runs on new commits.  
   - `pull_request` → Runs on PRs.  
3. **Jobs & Steps**:  
   - Jobs run **sequentially by default** (use `needs` for dependencies).  
   - Steps can **reuse actions** (e.g., `actions/checkout@v3`).  
4. **Security Integration**:  
   - SAST (SonarQube), SCA (Snyk), DAST (OWASP ZAP) can be automated.  

---

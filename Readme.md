# Jenkins-AnchoreGrype CI/CD Pipeline

## 🧾 Overview

This project provides a robust CI/CD pipeline implemented using **Jenkins** to automate the complete lifecycle of a containerized application. It covers build, test, code analysis, image scanning, and deployment tasks through integration with tools like **SonarQube**, **Jacoco**, **Anchore Grype**, and **Amazon ECR**.

---

## ✅ Prerequisites

Ensure the following components are available and configured:

- **Jenkins Server**: Properly installed and accessible Jenkins instance.
- **GitHub Repository**: Contains application code and Jenkinsfile (e.g., `Jenkins-AnchoreGrype`).
- **Maven**: Set up within Jenkins for Java-based builds.
- **SonarQube**: Accessible for static code analysis.
- **Anchore Grype**: Installed or integrated into the pipeline for Docker image scanning.
- **AWS Credentials**: Configured in Jenkins with access to Amazon ECR (if used).
- **GitHub Webhooks**: Configured to automatically trigger Jenkins jobs on commits or PRs.

---

## 🔌 Required Jenkins Plugins

| Plugin | Purpose |
|--------|---------|
| GitHub Plugin | Integrates Jenkins with GitHub repositories |
| Maven Integration Plugin | Enables Maven build steps |
| Pipeline Plugin | Enables use of Jenkins Pipelines |
| Docker Plugin | Builds and pushes Docker images |
| AWS ECR Plugin | Interfaces with AWS ECR |
| SonarQube Scanner Plugin | Connects to SonarQube for code quality checks |
| JUnit Plugin | Processes JUnit test reports |
| Jacoco Plugin | Generates code coverage reports |
| Pipeline AWS Plugin | Runs AWS actions from within Jenkins pipelines |

---

## 🧩 Pipeline Stages

The Jenkinsfile is designed to follow these key stages:

1. **Checkout Project**
   - Pulls the latest source code from GitHub.

2. **Build the Package**
   - Uses Maven to compile and package the application.

3. **Test**
   - Executes unit and integration tests using Maven.

4. **Code Analysis with Checkstyle**
   - Runs Checkstyle to ensure code style consistency.

5. **JUnit Tests**
   - Executes tests and publishes results using the JUnit plugin.

6. **Build & SonarQube Analysis**
   - Sends analysis to SonarQube with:
     - Project key, name, version
     - Source and binary directories
     - JUnit & Jacoco report paths

7. **Sonar Quality Gate Check**
   - Validates code quality against configured gates.

8. **Generate Jacoco Report**
   - (If enabled) Produces code coverage reports for review.

9. **Build Docker Image**
   - Uses Docker to build the container image from Dockerfile.

10. **Anchore Grype Scan**
    - Scans the Docker image for vulnerabilities.

11. **Deploy to Amazon ECR**
    - (Optional) Pushes Docker image to AWS ECR for deployment.

---

## 🛠 Key Tools & Functionality

### 🔍 Jacoco
A Java code coverage library generating detailed coverage reports for evaluating test effectiveness.

### 🛡 Anchore Grype
Open-source container image scanner for identifying vulnerabilities in Docker images.

### 📊 SonarQube
A code quality platform analyzing bugs, vulnerabilities, and code smells to enforce coding standards and maintainability.

### 🔄 Jenkins Triggers
GitHub webhooks automatically notify Jenkins on code changes (commits, PRs) to trigger pipeline runs.

---

## 🚀 Usage

1. Set up your Jenkins environment and required plugins.
2. Clone this repository and configure your own Jenkinsfile.
3. Set GitHub webhooks to trigger builds automatically.
4. Adjust environment-specific values (e.g., AWS region, ECR repo).
5. Trigger the pipeline via:
   - GitHub commit/PR
   - Manual run in Jenkins
6. Monitor pipeline logs and reports in Jenkins UI.

---

## 🧩 Example Jenkinsfile (High-Level)

> A full Jenkinsfile is included in the repository. Here's a high-level view:

```groovy
pipeline {
  agent any
  stages {
    stage('Checkout') { ... }
    stage('Build') { ... }
    stage('Test') { ... }
    stage('Checkstyle') { ... }
    stage('SonarQube Analysis') { ... }
    stage('Quality Gate') { ... }
    stage('Coverage Report') { ... }
    stage('Docker Build') { ... }
    stage('Grype Scan') { ... }
    stage('Deploy to ECR') { ... }
  }
}



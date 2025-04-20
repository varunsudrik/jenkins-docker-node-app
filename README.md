# jenkins-docker-node-app 🚀

This project is a sample backend application powered by **Node.js**, packaged with **Docker**, and deployed using a **CI/CD pipeline** with **Jenkins** and **SonarQube** for static code analysis.

---

## 📁 Project Structure

 ├── backend/ # Node.js backend source code │ ├── package.json │ ├── Dockerfile │ └── index.js (or main entry) ├── Jenkinsfile # CI/CD pipeline definition └── README.md


---

## 🚀 Features

- ⚙️ Node.js backend app
- 📦 Docker container support
- 🧪 SonarQube integration for code quality
- 🔁 Jenkins pipeline for CI/CD
- ☁️ Remote EC2 server deployment via SSH
- 🔐 Environment variable support for secrets

---

## 🛠️ Prerequisites

- [Docker](https://www.docker.com/)
- [Jenkins](https://www.jenkins.io/) with:
  - Docker Pipeline plugin
  - SSH Agent plugin
  - SonarQube Scanner plugin
- [SonarQube](https://www.sonarqube.org/)
- GitHub repository access

### Jenkins Credentials

- `dockerhub-creds` → DockerHub username/password
- `ec2-ssh` → SSH key to EC2 server
- `sonar-token` → SonarQube access token

---

## ⚙️ Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/varunsudrik/jenkins-docker-node-app.git
cd backend

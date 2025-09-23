# Simple Jenkins CI/CD Pipeline with Docker

## Objective
This project demonstrates a **basic CI/CD pipeline** using **Jenkins** and **Docker**.  
The pipeline automates the process of building, testing, and deploying an application whenever code changes are pushed to the repository.

---

## Tools & Technologies
- **Jenkins** – Continuous Integration/Delivery
- **Docker** – Containerization for build & deploy
- **GitHub/Git** – Source code repository

---

## Pipeline Stages
The Jenkins pipeline (`Jenkinsfile`) includes the following stages:

1. **Checkout**  
   - Pulls the latest code from the Git repository.

2. **Build**  
   - Builds a Docker image for the application.  
   - Example:  
     ```bash
     docker build -t my-app:latest .
     ```

3. **Test**  
   - Runs basic tests to verify the application.  
   - Example:  
     ```bash
     docker run --rm my-app:latest python -m unittest
     ```

4. **Deploy**  
   - Deploys the application container.  
   - Example:  
     ```bash
     docker run -d -p 5000:5000 my-app:latest
     ```

---

## Setup Instructions

### Install Jenkins
- Install Jenkins locally or use a cloud instance.  
- Install the required plugins:
  - Git Plugin  
  - Pipeline Plugin  
  - Docker Pipeline Plugin  

### Configure Jenkins
- Create a **new pipeline project** in Jenkins.  
- Link it to your GitHub repo.  
- Set webhook in GitHub to trigger Jenkins on **every push**.


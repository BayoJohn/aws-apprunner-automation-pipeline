# Apprunner-app
Demonstration of an automated deploment using Apprunner.
That is a fantastic way to approach a README! It frames the project as a **technical solution** rather than just a collection of files.

Here is a README structure designed around a "Scenario" and a "Justification" (The "Why") for each tool.






System Architecture
```mermaid
graph LR
    Local[Local Machine] --> Script[Bash Script]
    Script --> Docker[Docker Build]
    
    subgraph AWS_Cloud [AWS Cloud]
        Docker -- push --> ECR((Amazon ECR))
        ECR -- trigger --> AppRunner[AWS App Runner]
    end

    AppRunner --> Web((Live Website))




# AWS App Runner Deployment Pipeline

##  The Scenario

**The Challenge:** I had a Node.js application that needed to be deployed to a scalable, production-ready environment. The goal was to move away from manual server management (like EC2) and create a "push-button" deployment process where code updates could be containerized and shipped to the cloud automatically and securely.

---

##  The Toolchain: Why I Used Each Tool

### 1. Amazon ECR (Elastic Container Registry)

* **The Choice:** Instead of public Docker Hub, I used a private AWS ECR registry.
* **The "Why":** Since the application is hosted on AWS, using ECR provides the fastest and most secure way to store Docker images. It allows for fine-grained access control using **IAM roles**, ensuring that only my App Runner service can pull the images.

### 2. AWS App Runner

* **The Choice:** A fully managed container service.
* **The "Why":** I chose App Runner over ECS or EKS because it abstracts away the complex infrastructure. It automatically handles **load balancing, TLS/SSL certificates, and auto-scaling** without me having to configure a VPC or an Application Load Balancer manually. It’s the "Heroku experience" but inside the AWS ecosystem.

### 3. Bash Automation Script (`deploy.sh`)

* **The Choice:** A custom shell script to handle the build and push process.
* **The "Why":** Manual deployment is prone to human error (e.g., forgetting to tag an image correctly). The bash script ensures that every deployment is **consistent**. It automates:
* Authenticating the local environment with AWS.
* Building the container for the correct architecture.
* Pushing the image to ECR, which triggers the App Runner update.



### 4. Node.js

* **The Choice:** The application runtime.
* **The "Why":** Node.js was selected for its non-blocking I/O model, making it ideal for the lightweight, event-driven web services that App Runner is designed to host efficiently.

---

##  How it Works (Step-by-Step)

1. **Develop**: Make changes to the Node.js source code.
2. **Automate**: Run `./deploy.sh`.
* The script logs into AWS ECR.
* It builds the Docker image: `docker build -t node-app .`
* It tags and pushes the image to your private ECR URI.


3. **Deploy**: AWS App Runner detects the new image in ECR and performs a **rolling update**, ensuring zero downtime.

---

### How to use this for your repo:

1. **Open your `README.md**` file.
2. **Paste the content above**.
3. **Update the "How it Works" section** with your actual script name or any specific steps you took.
4. **Save and Push**:
```bash
git add README.md
git commit -m "docs: add scenario-based project overview"
git push origin main

```



**Would you like me to add a section on how you handled the AWS IAM permissions (the roles) for this scenario?**

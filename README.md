
Demonstration of an automated deploment using Apprunner.


![Whisk_4b403f7c72ce964a376441aa2ccb0a38dr](https://github.com/user-attachments/assets/bb7bcaf5-db5e-4a3d-b2a8-69396234eb83)




# 🚀 AWS App Runner Deployment Pipeline

[![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)](https://aws.amazon.com/)
[![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Node.js](https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org/)

## 📝 The Scenario
**The Challenge:** I had a Node.js application that needed to be deployed to a scalable, production-ready environment. The goal was to move away from manual server management (like EC2) and create a "push-button" deployment process where code updates could be containerized and shipped to the cloud automatically and securely.
<img width="1335" height="77" alt="Screenshot 2026-01-09 182054" src="https://github.com/user-attachments/assets/1572e254-754e-47e9-95f0-cdade57907c1" />
<img width="1314" height="325" alt="Screenshot 2026-01-09 182027" src="https://github.com/user-attachments/assets/1939e34d-5c1a-4567-b386-036ca7acbb01" />
<img width="1114" height="435" alt="Screenshot 2026-01-09 193138" src="https://github.com/user-attachments/assets/bb6b3274-3fac-4c6b-a789-1e7ee029ba4e" />
<img width="1080" height="405" alt="Screenshot 2026-01-09 184120" src="https://github.com/user-attachments/assets/eb33ec7c-932b-4690-b787-88f364c78f79" />
<img width="1070" height="252" alt="Screenshot 2026-01-09 184042" src="https://github.com/user-attachments/assets/e81e8994-33e9-4722-82ec-98e04975c4ca" />
<img width="621" height="347" alt="Screenshot 2026-01-09 183915" src="https://github.com/user-attachments/assets/52c6080f-a952-43bc-82bb-f04f5858ab1b" />

---

## 🏗️ Core Infrastructure & Justification

* **Amazon ECR (Elastic Container Registry):** I utilized a private AWS ECR registry over public alternatives to ensure maximum security and performance. By hosting the container images within the same AWS ecosystem as the application, I leveraged **IAM roles** for fine-grained access control, ensuring only authorized services like App Runner can pull images.
* **AWS App Runner:** This fully managed serverless service was selected to eliminate the overhead of managing EC2 instances or complex VPC configurations. It provides a streamlined "Heroku-like" experience within AWS, automatically handling **auto-scaling, load balancing, and SSL/TLS termination** right out of the box.
* **Bash Automation (`deploy.sh`):** To eliminate the risk of human error during manual deployments, I engineered a custom shell script to standardize the pipeline. This script automates the entire lifecycle—from AWS authentication and Docker building to image tagging and ECR pushing—ensuring every release is **consistent and repeatable**.
* **Node.js:** The application is built on Node.js to take advantage of its lightweight, event-driven architecture. This makes it a perfect fit for containerized environments, allowing for fast startup times and efficient resource utilization within the App Runner service.

---

## ⚙️ How it Works (Step-by-Step)

1.  **Develop**: Make changes to the Node.js source code locally.
2.  **Automate**: Run the `./deploy.sh` script.
    * The script authenticates with **AWS ECR**.
    * It builds the Docker image: `docker build -t node-app .`
    * It tags and pushes the image to your private ECR URI.
3.  **Deploy**: AWS App Runner detects the new image in ECR and performs a **rolling update**, ensuring zero downtime for the end user.


---

## 🚀 Getting Started

### Prerequisites
* **AWS CLI** installed and configured (`aws configure`).
* **Docker Desktop** running.
* An **ECR Private Repository** created in your AWS account.

### Installation
Clone the repository and prepare the script:
```bash
git clone [https://github.com/your-username/Apprunner-app.git](https://github.com/your-username/Apprunner-app.git)
cd Apprunner-app
chmod +x deploy.sh

# 🚀 Automated AWS App Runner Deployment Pipeline

![Whisk_4b403f7c72ce964a376441aa2ccb0a38dr](https://github.com/user-attachments/assets/bb7bcaf5-db5e-4a3d-b2a8-69396234eb83)

[![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white)](https://aws.amazon.com/)
[![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Node.js](https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org/)

## 📖 Project Overview
This repository demonstrates an automated, container-based deployment workflow using **AWS App Runner**. The project focuses on bridging the gap between local development and cloud production by utilizing a "push-button" deployment strategy. By containerizing a Node.js application and automating the delivery to **Amazon ECR**, this pipeline ensures a scalable, secure, and zero-infrastructure-management hosting environment.

<br>


## 🏗️ Core Infrastructure & Justification

* **Amazon ECR (Elastic Container Registry):** I utilized a private AWS ECR registry over public alternatives to ensure maximum security and performance. By hosting the container images within the same AWS ecosystem as the application, I leveraged **IAM roles** for fine-grained access control, ensuring only authorized services like App Runner can pull images.

<img width="1070" height="252" alt="Screenshot 2026-01-09 184042" src="https://github.com/user-attachments/assets/80539096-70e2-464f-ab63-324500d5e8a8" />
Figure 1: Private Amazon ECR repository setup with AES-256 encryption.

<br>
<br>


<img width="1080" height="405" alt="Screenshot 2026-01-09 184120" src="https://github.com/user-attachments/assets/8980dc4d-50ea-4dd8-9c34-69d302803e9b" />
Figure 2: Verified Docker image tags in the registry, ready for App Runner deployment.

<br>
<br>


  
* **AWS App Runner:** This fully managed serverless service was selected to eliminate the overhead of managing EC2 instances or complex VPC configurations. It provides a streamlined "Heroku-like" experience within AWS, automatically handling **auto-scaling, load balancing, and SSL/TLS termination** right out of the box.
<br>

* **Bash Automation:** To eliminate the risk of human error during manual deployments, I engineered a custom shell script to standardize the pipeline. This script automates the entire lifecycle—from AWS authentication and Docker building to image tagging and ECR pushing—ensuring every release is **consistent and repeatable**.
<br>

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


Demonstration of an automated deploment using Apprunner.


![Whisk_4b403f7c72ce964a376441aa2ccb0a38dr](https://github.com/user-attachments/assets/bb7bcaf5-db5e-4a3d-b2a8-69396234eb83)




# AWS App Runner Deployment Pipeline

##  The Scenario

**The Challenge:** I had a Node.js application that needed to be deployed to a scalable, production-ready environment. The goal was to move away from manual server management (like EC2) and create a "push-button" deployment process where code updates could be containerized and shipped to the cloud automatically and securely.


Core Infrastructure & Justification
Amazon ECR (Elastic Container Registry): I utilized a private AWS ECR registry over public alternatives to ensure maximum security and performance. By hosting the container images within the same AWS ecosystem as the application, I leveraged IAM roles for fine-grained access control, ensuring only authorized services like App Runner can pull images.

AWS App Runner: This fully managed serverless service was selected to eliminate the overhead of managing EC2 instances or complex VPC configurations. It provides a streamlined "Heroku-like" experience within AWS, automatically handling auto-scaling, load balancing, and SSL/TLS termination right out of the box.

Bash Automation (deploy.sh): To eliminate the risk of human error during manual deployments, I engineered a custom shell script to standardize the pipeline. This script automates the entire lifecycle—from AWS authentication and Docker building to image tagging and ECR pushing—ensuring every release is consistent and repeatable.

Node.js: The application is built on Node.js to take advantage of its lightweight, event-driven architecture. This makes it a perfect fit for containerized environments, allowing for fast startup times and efficient resource utilization within the App Runner service.

##  How it Works (Step-by-Step)

1. **Develop**: Make changes to the Node.js source code.
2. **Automate**: Run `./deploy.sh`.
* The script logs into AWS ECR.
* It builds the Docker image: `docker build -t node-app .`
* It tags and pushes the image to your private ECR URI.


3. **Deploy**: AWS App Runner detects the new image in ECR and performs a **rolling update**, ensuring zero downtime.



🚀 Getting Started
Prerequisites
AWS CLI installed and configured (aws configure).

Docker Desktop running.

An ECR Private Repository created in your AWS account.

Installation
Clone the repository:

Bash

git clone https://github.com/your-username/Apprunner-app.git
cd Apprunner-app
Make the deployment script executable:

Bash

chmod +x deploy.sh
Usage
To deploy your application to the cloud, simply run:

Bash

./deploy.sh
🔐 Security Features
Fail-Fast Logic: The script uses set -e to stop immediately if any stage (build/push) fails.

Private ECR: Images are stored in a private registry, protected by AWS IAM permissions.

Minimal Base Image: Uses node:alpine to reduce the attack surface and image size.

📈 Future Improvements
[ ] Integrate GitHub Actions for fully automated "Push-to-Deploy" functionality.

[ ] Add AWS CloudWatch alarms for automatic error notification.

[ ] Implement Snyk image scanning in the deploy.sh script to check for vulnerabilities.

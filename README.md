# Mini WeTransfer - Secure & Temporary File Sharing

A secure, temporary file-sharing web application designed and deployed using modern Cloud and DevOps practices. This project demonstrates end-to-end automation, infrastructure as code, and containerized deployment.

## 🌟 Key Features
- **Secure File Uploads:** Direct uploads to AWS S3.
- **Fast & Responsive UI:** Built with React and Vite.
- **Automated Deployments:** CI/CD pipelines powered by GitHub Actions.
- **Infrastructure as Code:** Fully automated AWS provisioning using Terraform.
- **Containerized:** Both frontend and backend are containerized using Docker and orchestrated with Docker Compose.

## 🛠️ Technology Stack
### Frontend
- React.js (Vite)
- Nginx (for serving static files in production)

### Backend
- Node.js & Express
- AWS SDK

### Cloud & Infrastructure (AWS)
- **EC2 (Elastic Compute Cloud):** Hosts the Dockerized application.
- **S3 (Simple Storage Service):** Stores the uploaded files securely.
- **DynamoDB:** Fast NoSQL database tracking file metadata and links.

### DevOps & Automation
- **Terraform:** Used to provision the S3 bucket, DynamoDB table, Security Groups, and EC2 instance.
- **Docker & Docker Compose:** Containerization and local orchestration.
- **GitHub Actions:** Continuous Integration (CI) and Continuous Deployment (CD) pipeline.

## 🏗️ System Architecture
1. **Developer Push:** Code is pushed to the `main` branch.
2. **GitHub Actions:** Triggers the deployment pipeline.
3. **EC2 Deployment:** The pipeline connects to the EC2 instance via SSH, pulls the latest code, and rebuilds the Docker containers.
4. **App Execution:** The React frontend and Node.js backend run as interconnected Docker containers. The backend securely interfaces with AWS S3 and DynamoDB to handle file transfers.

## 🚀 Local Development Setup

To run this project locally, ensure you have Docker and Docker Compose installed.

1. **Clone the repository:**
   ```bash
   git clone https://github.com/niladri17dutta/Mini-WeTransfer-Secure-Temporary-File-Sharing-App.git
   cd Mini-WeTransfer-Secure-Temporary-File-Sharing-App
   ```

2. **Configure Environment Variables:**
   Update the `backend/.env` file with your AWS credentials:
   ```env
   PORT=5000
   AWS_ACCESS_KEY_ID=your_access_key
   AWS_SECRET_ACCESS_KEY=your_secret_key
   AWS_REGION=us-east-1
   S3_BUCKET_NAME=miniwetransfer-uploads-nilad-demo-123
   DYNAMODB_TABLE_NAME=MiniWeTransferFiles
   ```

3. **Start the containers:**
   ```bash
   docker-compose up --build
   ```

---

## 👨‍💻 Author
- Niladri Dutta   

---

# AWS Assignment 6: Flask Backend & Express Frontend on AWS ECS Fargate

This project contains a containerized **Flask backend** and an **Express frontend** application deployed on AWS using **Amazon ECR**, **ECS Fargate**, **VPC**, **Security Groups**, and **CloudFormation**.

---

## Project Folder Structure

```text
aws-ecr-ecs-task/
│
├── backend/                  # Flask Backend Application
│   ├── myenv/                # Python virtual environment
│   ├── app.py                # Main Flask application file
│   ├── Dockerfile            # Dockerfile for Flask
│   └── requirements.txt      # Python dependencies
│
├── frontend/                 # Express Frontend Application
│   ├── node_modules/         # Node.js dependencies
│   ├── public/               # Public assets
│   ├── Dockerfile            # Dockerfile for Express
│   ├── package-lock.json     # Node lock file
│   ├── package.json          # Node.js dependencies
│   └── server.js             # Main Express server file
│
├── infrastructure\cloudformation/  # AWS CloudFormation Templates
│   ├── ecr/                  # ECR setup stack
│   │   └── ecr-repositories.yaml
│   ├── ecs/                  # ECS Clusters, Tasks, and Services
│   │   ├── backend-service-stack.yaml
│   │   ├── backend-task-stack.yaml
│   │   ├── cluster.yaml
│   │   ├── frontend-service-stack.yaml
│   │   └── frontend-task-stack.yaml
│   └── network/              # VPC & Security Groups setup
│       └── vpc.yaml
│
├── .env.example              # Environment variables template
├── .gitignore                # Git ignore file
├── docker-compose.yaml       # Local multi-container testing
└── README.md                 # Project documentation
## Architecture Deployment Steps

1. **Create ECR Repositories** *(CloudFormation: `ecr-repositories.yaml`)*
2. **Build Docker Images Locally**
   * **Backend:** Flask (Runs on port `9000`)
   * **Frontend:** Express (Runs on port `8000`)
3. **Push Docker Images** to Amazon ECR repositories
4. **Create VPC & Networking** *(CloudFormation: `vpc.yaml`)*
   * Custom VPC with 2 Public Subnets
   * Internet Gateway & Route Tables
   * Security Groups: Backend SG (Port `9000`) & Frontend SG (Port `8000`)
5. **Create ECS Cluster** *(CloudFormation: `cluster.yaml`)*
   * Setup AWS ECS Fargate Cluster
6. **Create Task Definitions**
   * Backend Task (`backend-task-stack.yaml`)
   * Frontend Task (`frontend-task-stack.yaml` - includes environment variables, logging, and health checks)
7. **Create ECS Services**
   * Backend Service (`backend-service-stack.yaml`)
   * Frontend Service (`frontend-service-stack.yaml`)

---

## Live Application Endpoints

* **Frontend Application:** [http://52.66.240.170:8000]
* **Backend API:** [http://15.206.209.45:9000]
* **Backend Health Check:** [http://15.206.209.45:9000/health]

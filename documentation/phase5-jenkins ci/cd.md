#### commands used
sudo systemctl start jenkins
sudo systemctl status jenkins
docker build -t agamtyagi/xqora-nginx:v1 .
docker images
kind load docker-image agamtyagi/xqora-nginx:v1 --name devops
helm upgrade --install nginx ./nginx
kubectl get pods
kubectl get deployments
kubectl get svc
kubectl get nodes
kubectl logs <pod-name>
kubectl describe pod <pod-name>
kubectl rollout restart deployment nginx
kubectl rollout status deployment nginx


############################################


Phase 5: Continuous Integration and Continuous Deployment (CI/CD) with Jenkins
Objective

The objective of this phase was to automate the software delivery process using Jenkins. A CI/CD pipeline was designed to automatically fetch the latest source code from GitHub, build a Docker image, and deploy the application to a Kubernetes cluster using Helm. This reduces manual effort, ensures consistency, and enables faster, more reliable deployments.

Introduction

Continuous Integration (CI) is the practice of frequently integrating code changes into a shared repository, where automated builds and tests are executed to detect issues early.

Continuous Deployment (CD) extends CI by automatically deploying successfully built applications to the target environment, making software releases faster and more reliable.

Jenkins is an open-source automation server widely used for implementing CI/CD pipelines. It supports integration with numerous DevOps tools through plugins.

Jenkins

Jenkins is an automation server used to automate repetitive development tasks such as:

Source code checkout
Application build
Testing
Docker image creation
Deployment
Monitoring pipeline execution

It uses pipelines to define the sequence of stages required for software delivery.

Jenkins Pipeline

A Jenkins Pipeline is a collection of automated stages that define the application's build and deployment workflow.

Typical stages include:

Source Code Checkout
Build
Test
Package
Deploy
Verification

Pipelines are written using Groovy in a file called Jenkinsfile.

Role of GitHub

GitHub serves as the version control repository for the application source code.

Jenkins connects to GitHub to:

Clone the repository
Retrieve the latest code changes
Trigger automated builds after code updates

This integration ensures that deployments always use the latest version of the application.

Docker Integration

Docker is used to package the application and its dependencies into a lightweight, portable container image.

Benefits include:

Environment consistency
Easy application distribution
Faster deployment
Simplified dependency management

Each successful pipeline execution generates a new Docker image.

Kubernetes Deployment

Kubernetes is responsible for managing and running containerized applications.

Its responsibilities include:

Scheduling containers
Maintaining desired replicas
Automatic restarts
Load balancing
Self-healing

Deploying through Kubernetes ensures high availability and scalability.

Helm

Helm is the package manager for Kubernetes.

Instead of manually creating Kubernetes resources, Helm packages them into reusable Charts.

Advantages of Helm include:

Simplified deployments
Easy upgrades
Version management
Rollback support
Configuration through values files
CI/CD Workflow

The automated workflow follows these steps:

Developer pushes code to GitHub.
Jenkins detects the new changes.
Jenkins clones the repository.
The application is built.
A Docker image is created.
The image is made available to the Kubernetes cluster.
Helm deploys or updates the application.
Kubernetes creates or updates the required Pods and Services.
Jenkins verifies the deployment status.
Benefits of CI/CD
Eliminates repetitive manual tasks.
Detects integration issues early.
Ensures consistent deployments.
Reduces deployment time.
Improves software quality.
Enables rapid release cycles.
Minimizes human error.
Provides repeatable and reliable deployments.
Tools Used
GitHub
Jenkins
Git
Docker
Kubernetes
Helm
Kind (Local Kubernetes Cluster)
Ubuntu/WSL
Learning Outcomes

After completing this phase, the following concepts were understood:

Principles of Continuous Integration and Continuous Deployment.
Jenkins architecture and pipeline execution.
Integration of Jenkins with GitHub.
Automated Docker image creation.
Kubernetes application deployment.
Helm-based application management.
End-to-end CI/CD workflow automation.
Monitoring and troubleshooting deployment pipelines.
Conclusion

This phase demonstrated the implementation of a complete CI/CD pipeline using Jenkins. By integrating GitHub, Docker, Kubernetes, and Helm, the software delivery process became automated, repeatable, and efficient. The pipeline reduced manual intervention, accelerated deployments, and established a foundation for modern DevOps practices.
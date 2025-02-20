# Jenkins Pipeline for Docker-Based Deployment

## Overview

This project automates the deployment of a Docker-based application using Jenkins. The pipeline performs the following steps:

1. Cleans up any existing Docker resources on the remote server.
2. Clones the latest code from the Git repository.
3. Builds and deploys a Docker image.
4. Initializes a Docker Swarm cluster and deploys a stack.
5. Runs a security scan using Nikto.
6. Sends an email notification with the scan results.

## Prerequisites

Ensure that the following requirements are met before running the pipeline:

- **Jenkins** installed with the following plugins:
  - Pipeline
  - SSH Agent Plugin
  - Email Extension Plugin
- **A Remote Server** with:
  - Docker and Docker Compose installed
  - SSH access enabled
- **Nikto** installed on the Jenkins server
- **Valid Email Configuration** in Jenkins for notifications

## Environment Variables

The pipeline uses the following environment variables:

| Variable Name           | Description                                              |
| ----------------------- | -------------------------------------------------------- |
| `GIT_REPO_URL`          | Git repository URL                                       |
| `GIT_BRANCH`            | Branch to be cloned                                      |
| `DOCKER_IMAGE_NAME`     | Name of the Docker image                                 |
| `DOCKER_CONTAINER_NAME` | Name of the Docker container                             |
| `REMOTE_SERVER`         | SSH access to the remote server                          |
| `SSH_CREDENTIALS_ID`    | Jenkins credential ID for SSH authentication             |
| `APP_DIR`               | Directory on the remote server to deploy the application |
| `WEBSITE_DIR`           | Website directory in the project                         |
| `DEVELOPER_EMAIL`       | Email(s) to receive notifications                        |
| `TARGET_URL`            | Target URL for the security scan                         |
| `OUTPUT_FILE`           | File to store security scan results                      |

## Pipeline Stages

### 1. Clean Up Docker Environment

- Stops and removes all running and stopped Docker containers.
- Removes all Docker images.
- Removes any existing Docker stack and leaves Docker Swarm.

### 2. Clone Repository on Remote Server

- Clones the specified Git repository branch to the remote server.
- If the repository already exists, resets and pulls the latest changes.

### 3. Build and Deploy Docker Image

- Copies necessary files to the remote server.
- Builds a new Docker image from the source code.
- Initializes Docker Swarm.
- Deploys the Docker stack using `docker-compose.yml`.

### 4. Verify Deployment

- Checks the status of the deployed Docker stack.

### 5. Run Nikto Security Scan

- Performs a security scan on the deployed application.
- Stores the scan results in an HTML file.

## Notifications

### On Success:

- Sends an email notification with details of the deployment.
- Attaches the security scan report.

### On Failure:

- Sends an email notification with error logs for troubleshooting.

## Cleanup Process

- Regardless of success or failure, the pipeline ensures that unnecessary Docker resources are removed from the remote server.

## How to Use

1. Configure Jenkins with the necessary credentials.
2. Set up the required environment variables.
3. Trigger the pipeline manually or configure it for automatic execution.

## Contact

For any issues or contributions, feel free to submit a pull request or contact the developer at `9890623352q@gmail.com`.


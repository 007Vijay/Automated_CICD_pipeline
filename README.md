This Jenkins-based CI/CD pipeline automates code integration, deployment, and security scanning using Docker, GitHub, and Nikto on a remote Ubuntu server. It cleans up old containers, pulls the latest code, builds a new Docker image, and deploys using Docker Swarm. A Nikto security scan generates a report, and automated email notifications update developers on success or failure. Finally, Docker cleanup optimizes resources, ensuring efficient, secure, and reliable deployments.

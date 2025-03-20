# 🖥️ Getting Started with Localstack 📚

Localstack offers a comprehensive, local AWS simulation, providing developers opportunities to build, test, profile, and debug their cloud-based systems entirely offline and potentially for free. This activity provides a tutorial to get started with LocalStack setup and a functionality demonstration.

**Disclaimer:** This activity uses Windows 10/11 OS.

## 📋 Requirements
1. [VS Code](https://code.visualstudio.com/download)
2. [Docker](https://docs.docker.com/desktop/setup/install/windows-install/)
   - Verify with `docker -v and docker-compose -v` in Command Prompt
4. [Commandeer](https://getcommandeer.com/download-app)
5. [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
   - Verify with `aws --version` in Command Prompt
   - For initial credential set up, enter `aws configure` and fill up the following sequentially: `test, test, ap-southeast-1, json`
   
## 🎯 Objectives
1. Set up LocalStack with Docker.
2. Verify LocalStack Instance with Browser, Docker, and Commandeer.
3. Demonstrate LocalStack functionality with AWS S3.

## Part 1: Set up LocalStack with Docker
1. Create a folder named `docker-compose-localstack` in your preferred directory and open it with VS Code

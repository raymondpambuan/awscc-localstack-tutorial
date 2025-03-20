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
1. Open Docker Desktop.
2. Create a folder named `docker-compose-localstack` in your preferred directory and open it with VS Code
3. Create a file named `docker-compose.yml` and copy the following contents:
   
   <pre>
   version: '3.1'

   services:
   
     localstack:
       image: localstack/localstack:latest
       environment:
         - AWS_DEFAULT_REGION=ap-southeast-1
         - EDGE_PORT=4566
         - SERVICES=lambda,s3,ec2
       ports:
         - '4566-4583:4566-4583'
       volumes:
         - "${LOCALSTACK_VOLUME_DIR:-./volume}:/var/lib/localstack"
         - "/var/run/docker.sock:/var/run/docker.sock"
   </pre>

4. To launch the LocalStack instance, open a terminal in VS Code and enter `docker-compose up`. The output should contain details about the instance. The information about the running instance can also be viewed in `Docker` desktop.

## Part 2: Verify LocalStack Instance with Browser and Commandeer
1. To verify if the LocalStack is running correctly, open a browser and enter `http://localhost:4566/_localstack/health`.
2. Optionally, you can enter `http://localhost.localstack.cloud:4566/_localstack/swagger` to view the user interface of LocalStack with swagger.
3. Open `Commandeer` and set up the account. Use the following settings for configuring the account:
   - Account Type: LocalStack
   - Region: ap-southeast-1
   - LocalStack URL: http://localhost:4566
   - Keep the rest of the settings default
4. For the name, follow the format [nickname]-awsccmu-localstack.
5. Refresh Commandeer and allow firewall.
6. In VS Code, create a new terminal and enter `aws --endpoint-url=http://localhost:4566 s3 mb s3://awscc-mu-demo` to create a local S3 bucket.
7. Go back to Commandeer, and under `AWS > S3 > Dashboard`, there should be a bucket created.
8. Go back to VS Code and create a file `test.txt`. Enter any text to the file and save it.

## Part 3: Demonstrate LocalStack functionality with AWS S3
1. In the VS Code terminal, enter `aws --endpoint-url=http://localhost:4566 s3 cp test.txt s3://awscc-mu-demo` to add the file to the local S3 bucket.
2. In Commandeer, click refresh and verify if the text file was added.
3. Go back to VS Code and in the terminal, enter `aws --endpoint-url=http://localhost:4566 s3 ls s3://awscc-mu-demo` to list the contents of the bucket and verify if the file was added.

## (Optional) Part 4: Clean up
1. If you want to uninstall the software, type the keyboard shortcut `Win + R` and enter `appwiz.cpl`. Search for the installed applications, select the application and click `Uninstall`.

![image](https://github.com/user-attachments/assets/7a25dca3-3c38-4174-b8e2-3317e259db34)

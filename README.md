# 🖥️ Getting Started with LocalStack 📚

LocalStack offers a comprehensive, local AWS simulation, providing developers opportunities to build, test, profile, and debug their cloud-based systems entirely offline and potentially for free. This activity provides a tutorial to get started with LocalStack setup and a functionality demonstration.

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
2. Verify LocalStack Instance with Browser and Commandeer.
3. Demonstrate LocalStack functionality with AWS S3.

## Part 1: Set up LocalStack with Docker
1. Open Docker Desktop.
2. Create a folder named `docker-compose-localstack` in your preferred directory and open it with VS Code.
3. Create a file named `docker-compose.yml` and copy the following file contents then save:
   
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

4. To launch the LocalStack instance, open a terminal in VS Code and enter `docker-compose up`. The output should contain details about the instance. The information about the running instance can also be viewed in `Docker` desktop. **Screenshot this similar to the image below**.
   
![image](https://github.com/user-attachments/assets/f5d793cf-ac83-4aac-ac91-9721f3140bda)

## Part 2: Verify LocalStack Instance with Browser and Commandeer
1. To verify if the LocalStack is running correctly, open a browser and enter `http://localhost:4566/_localstack/health`. There should be AWS services listed and its status in LocalStack. **Screenshot this page**.
2. Optionally, you can enter `http://localhost.localstack.cloud:4566/_localstack/swagger` to view the user interface of LocalStack API with OpenAPI and swagger.
3. Open `Commandeer` and set up the account. Use the following settings/entries for configuring the account:
   - Account Type: LocalStack
   - Region: ap-southeast-1
   - LocalStack URL: http://localhost:4566
   - Both Access Keys: test
   - Name format: `[nickname]-awsccmu-localstack`
   - Keep the rest of the settings default
4. Refresh Commandeer and allow firewall if prompted.

![image](https://github.com/user-attachments/assets/322165d6-6ff5-4a21-a248-49e76d35842d)

5. To verify if LocalStack is connected to Commandeer, the indicator for Docker and LocalStack in the top-right of the UI should be green.

![image](https://github.com/user-attachments/assets/7ec88ed6-937b-41bf-9cc5-0fd9d2dad0c6)

## Part 3: Demonstrate LocalStack functionality with AWS S3
1. In VS Code, create a new terminal and enter `aws --endpoint-url=http://localhost:4566 s3 mb s3://awscc-mu-demo` to create a local S3 bucket using the AWS CLI command structure and specific make bucket command `mb`.
2. Go back to Commandeer, and under `AWS > S3 > Dashboard`, there should be a bucket created. **Screenshot this page**.

![image](https://github.com/user-attachments/assets/3f21013c-4230-4aea-85b0-2fe5e6c8c1fa)

3. Go back to VS Code and create a file `test.txt`. Enter any text to the file and save it.

![image](https://github.com/user-attachments/assets/f2f4a609-21ef-4377-958f-21cd900d9d7e)

5. In the recently created terminal, enter `aws --endpoint-url=http://localhost:4566 s3 cp test.txt s3://awscc-mu-demo` to add the file to the local S3 bucket using the `cp` or copy command of AWS CLI.
6. In Commandeer, click refresh and verify if the text file was added. View the contents of the text file and it should match with what you added. **Screenshot this page**.

![image](https://github.com/user-attachments/assets/051082bd-7982-4b4f-9272-d0a896352ccc)

8. Go back to VS Code and in the terminal, enter `aws --endpoint-url=http://localhost:4566 s3 ls s3://awscc-mu-demo` to list the contents of the bucket using the `ls` command and verify if the file was added. **Screenshot this terminal**.

## (Optional) Part 4: Clean up
1. In the terminal where Docker was launched, enter the keyboard shortcut `Ctrl + C` to stop the LocalStack instance. Verify it by viewing Docker Desktop.
2. If you want to save up space and will not develop with LocalStack in the future, go to `Docker Desktop`, and under `Containers`, select the existing instance(s) and click `Delete`.

![image](https://github.com/user-attachments/assets/49a42ad4-65bb-4f2a-ac9f-0f0b45fd4523)

4. If you want to uninstall the software, type the keyboard shortcut `Win + R` and enter `appwiz.cpl`. Search for the installed applications, select the application and click `Uninstall`.

![image](https://github.com/user-attachments/assets/7a25dca3-3c38-4174-b8e2-3317e259db34)

## Authors
### Activity and Code Materials Prepared by:
- [Onexlab](https://youtu.be/Bytw73GvRHA?si=vtb3nx4eLh1mY6op)
### Learning Material Prepared by:
- Raymond Irwin Pambuan (raymondpambuan)

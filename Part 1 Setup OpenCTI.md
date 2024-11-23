# CTI Integration

## Objective

OpenCTI is an open-source platform designed for managing and analyzing Cyber Threat Intelligence (CTI). Having a centralized location to manage all of your CTI data is a great way to correlate observables that you may come across in your environment such as an IP, domain, or file hash. Part 1 of this series will walk you through how to install OpenCTI on your virtual machine. Two prerequisites for installation are two Ubuntu server's, one for a Splunk server and the other for the OpenCTI server. If you do not know how to install a Ubuntu Server please visit my <a href="https://github.com/wesgough/ubuntu-install">Ubuntu-Install</a> repository for a step-by-step guide.

### Skills Learned

- Advanced understanding of SIEM concepts and practical application.
- Proficiency in analyzing and interpreting network logs.
- Ability to generate and recognize attack signatures and patterns.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used

- Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Network analysis tools (such as Wireshark) for capturing and examining network traffic.
- Telemetry generation tools to create realistic network traffic and attack scenarios.

## Step-By-Step Guide

1) To begin let's SSH into our Ubuntu Server so we have copy/paste capabilities and install Docker. Docker is an open-source platform that allows developers to build, test, and deploy applications quickly and we will be using this to spin up OpenCTI.
```
sudo apt-get update && sudo apt-get upgrade -y
```
```
sudo apt install docker-compose
```

![1](https://github.com/user-attachments/assets/8ba299c0-b420-4659-92e0-c86bab5d9b85)

*Ref 1: Docker-Compose Install* 

2) Now lets head over to OpenCTI's github to clone the repository: https://github.com/OpenCTI-Platform/docker.git. Scroll down and click "OpenCTI documentation space" and then clone the repository.

![1](https://github.com/user-attachments/assets/9655bea0-fc17-42a7-97ea-bf9bcfdae87c)
![2](https://github.com/user-attachments/assets/e9a0a4b9-ca84-44c0-bd49-397ff490ee87)

*Ref 2: OpenCTI Repository*

3) Head back over to our SSH terminal and run the command.
```
git clone https://github.com/OpenCTI-Platform/docker.git
```
![1](https://github.com/user-attachments/assets/6f7f63b7-6833-49b8-8c47-fc2b48bd7549)

*Ref 3: Install Repo*

4) The docker-compose.yml file will contain all the configurations that Docker will reference. This file references a hidden file called .env.sample, type the following commands to see and open the file. The variables inside the docker-compose.yml file will get pulled from the .env.sample file.
```
ls -la
```
```
cat .env.sample
```
```
mv .env.sample .env
```
![1](https://github.com/user-attachments/assets/7b14411c-96ad-478c-8972-cd6416d1b1aa)

*Ref 4: Docker-Compose.yml*

5) Lets open up the .env.sample file with nano and change the configurations. For the Admin_Token field head over to https://www.uuidgenerator.net/ and copy/paste the UUID. Change the base url to the ip address of our Ubuntu Server, and change all the passwords as well.
```
nano .env
```

![1](https://github.com/user-attachments/assets/29ceb8ec-e07d-4ffa-a236-e62238599bbc)

![1](https://github.com/user-attachments/assets/64485194-d949-42a7-b034-6f3ef765b1b8)

*Ref 5: Configuration*

6) Now that we have updated our environment variables, the last thing we need to update is for Elastic. This assigns a static map count for Elastic and helps with memory. With all the configurations done, we can now start up Docker.
```
sudo sysctl -w vm.max_map_count=1048575
```
```
sudo systemctl start docker.service
```
```
sudo docker-compose up -d
```

*Ref 6: Start Docker Service*

7) 



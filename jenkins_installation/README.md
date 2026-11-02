# Jenkins Installation Guide

This content explains the steps to install Jenkins.

## Description

This file contains the steps for the following activities. Completing them will let us use Jenkins.

- **A.** Create an EC2 Instance with proper security group settings
- **B.** Login to EC2 Instance
- **C.** Install Java
- **D.** Validate the JDK & Jenkins Versions
- **E.** Add Jenkins Repository & GPG Key
- **F.** Install Jenkins
- **G.** Enable & Start Jenkins Service
- **H.** Unlock Jenkins in the Web Browser
- **I.** Install Plugins
- **J.** Use Jenkins

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [A. Create an EC2 Instance with proper security group settings](#a-create-an-ec2-instance-with-proper-security-group-settings)
- [B. Login to EC2 Instance](#b-login-to-ec2-instance)
- [C. Install Java](#c-install-java)
- [D. Validate the JDK & Jenkins Versions](#d-validate-the-jdk--jenkins-versions)
- [E. Add Jenkins Repository & GPG Key](#e-add-jenkins-repository--gpg-key)
- [F. Install Jenkins](#f-install-jenkins)
- [G. Enable & Start Jenkins Service](#g-enable--start-jenkins-service)
- [H. Unlock Jenkins in the Web Browser](#h-unlock-jenkins-in-the-web-browser)
- [I. Install Plugins](#i-install-plugins)
- [J. Use Jenkins](#j-use-jenkins)
- [Troubleshooting](#troubleshooting)
- [References](#references)

---

## Prerequisites

<!-- TODO: List prerequisites (e.g., AWS account, key pair, security group access, etc.) -->
1. An AWS account. If you don’t have one, you can register here -> (https://portal.aws.amazon.com/billing/signup#/start).

2. An Amazon EC2 key pair. If you don’t have one, refer to Creating a key pair -> (https://www.jenkins.io/doc/tutorials/tutorial-for-installing-jenkins-on-AWS/#creating-a-key-pair).

3. An AWS IAM User with programmatic key access and permissions to launch EC2 instances -> (https://plugins.jenkins.io/ec2/#plugin-content-iam-setup)
---

## A. Create an EC2 Instance with proper security group settings

<!-- TODO: Add detailed steps -->
Configure Security Group:
1. Sign in to the AWS Management Console.
2. Open the Amazon EC2 console by selecting EC2 under Compute.
3. In the left-hand navigation bar, select Security Groups, and then select Create Security Group.
4. In Security group name, enter devopsSG1 or any preferred name of your choice, and provide a description.
5. Select your VPC from the list. You can use the default VPC.
6. On the Inbound tab, add the rules as follows:
  >Select Add Rule, and then select SSH from the Type list.
  
  >Under Source, select Custom, and in the text box, enter the IP address 0.0.0.0/0.
  
  >Select Add Rule, and then select HTTP from the Type list.
  
  >Select Add Rule, and then select Custom TCP Rule from the Type list.
  
  >Under Port Range, enter 8080.
7. Select Create. 

Launch EC2 Instance:
1. Sign in to the AWS Management Console.
2. Open the Amazon EC2 console by selecting EC2 under Compute.
3. From the Amazon EC2 dashboard, select Launch Instance.
4. The Choose an Amazon Machine Image (AMI) page displays a list of basic configurations called Amazon Machine Images (AMIs) that serve as templates for your instance. Select - "Ubuntu Server 26.04 LTS (HVM), SSD Volume Type" that has the AMI value - ami-0d97d7f07b25dd693
5. Scroll down and select the key pair you created in the creating a key pair section above or any existing key pair you intend to use.
6. Select Select an existing security group. Select the devopsSG1 security group that you created.
  Select Launch Instance.
7. In the left-hand navigation bar, choose Instances to view the status of your instance. Initially, the status of your instance is pending. After the status changes to running, your instance is ready for use.
---

## B. Login to EC2 Instance

<!-- TODO: Add detailed steps -->
1. Open a terminal or PowerShell window.
2. Use the ssh command to connect to the instance. You will specify the private key (.pem) file and ec2-user@public_dns_name. The command is provided in "Connect" -> In SSH Client.
```bash
ssh -i "devopskey1.pem" ubuntu@ec2-54-196-134-190.compute-1.amazonaws.com
```
3. Enter yes.

---

## C. Install Java

<!-- TODO: Add detailed steps -->

```bash
sudo apt update
sudo apt install -y fontconfig openjdk-21-jre
java -version
```

---

## D. Validate the JDK & Jenkins Versions

<!-- TODO: Add detailed steps -->
Current Active Releases Overview for JDK. We are using JDK21
| Version | Release Type | Latest Patch Version | Release Date |
|---------|--------------|----------------------|--------------|
| JDK 27 | Short-Term (Latest Stable) | 27.0.1 | September 2026 |
| JDK 25 | Long-Term Support (Latest LTS) | 25.0.5 | September 2025 |
| JDK 21 | Long-Term Support (Prior LTS) | 21.0.13 | September 2023 |
| JDK 17 | Long-Term Support | 17.0.21 | September 2021 |

The latest stable (Long-Term Support, or LTS) Jenkins version is 2.580.2. We are using 

---

## E. Add Jenkins Repository & GPG Key

<!-- TODO: Add detailed steps -->

```bash
sudo apt update

sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2026.key

echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/" | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
```

---

## F. Install Jenkins

<!-- TODO: Add detailed steps -->

```bash
sudo apt update
sudo apt install -y jenkins
```

---

## G. Enable & Start Jenkins Service

<!-- TODO: Add detailed steps -->

```bash
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

---

## H. Unlock Jenkins in the Web Browser

<!-- TODO: Add detailed steps -->
1. Open your browser and navigate to http://<YOUR_EC2_PUBLIC_IP>:8080.
2. Retrieve the initial administrator password from your server:
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

---

## I. Install Plugins

<!-- TODO: Add detailed steps -->

---

## J. Use Jenkins

<!-- TODO: Add detailed steps -->

---

## Troubleshooting

<!-- TODO: Add common issues and their fixes -->

| Issue | Possible Cause | Fix |
|-------|----------------|-----|
|       |                |     |

---

## References

<!-- TODO: Add links to official documentation -->

# Gaining operational insights with AIOps using Amazon DevOps Guru

This lab is provided as part of **[AWS Innovate Data And AI/ML Edition](https://aws.amazon.com/events/aws-innovate/apj/aiml-data/)**.

ℹ️ You will run this lab in your own AWS account. Please follow directions at the end of the lab to remove resources to avoid future costs.

## **Overview**
[Amazon DevOps Guru](https://aws.amazon.com/devops-guru/) offers a fully managed AIOps platform service that enables developers and operators to improve application availability and resolve operational issues faster. It minimizes manual effort by leveraging machine learning (ML) powered recommendations. DevOps Guru automatically detects operational issues, predicts impending resource exhaustion, details likely causes, and recommends remediation actions.

This is a labified version of this [AWS Blog](https://aws.amazon.com/blogs/devops/gaining-operational-insights-with-aiops-using-amazon-devops-guru/)

It will walk you through how to enable DevOps Guru for your account in a typical serverless environment and observe the insights and recommendations generated for various activities. These insights are generated for operational events that could pose a risk to your application availability. DevOps Guru uses [AWS CloudFormation](http://aws.amazon.com/cloudformation) stacks as the application boundary to detect resource relationships and co-relate with deployment events.

## Setup
### Create Cloud9 environment via AWS CloudFormation

1. Log in your AWS Account
1. Click [this link](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=DevOpsGuru&templateURL=https://awsinnovatedata2022.s3.amazonaws.com/devopsguru/cloud9.yaml) and open a new browser tab
1. Click *Next* again to the stack review page, tick **I acknowledge that AWS CloudFormation might create IAM resources** box and click *Create stack*.
  ![Acknowledge Stack Capabilities](/images/acknowledge-stack-capabilities.png)
1. Wait for a few minutes for stack creation to complete.
1. Select the stack and note down the outputs (*Cloud9EnvironmentId* & *InstanceProfile*) on *outputs* tab for next step.
  ![Cloud9 Stack Output](/images/stack-cloud9-output.png)

### Assign instance role to Cloud9 instance

1. Launch [AWS EC2 Console](https://console.aws.amazon.com/ec2/v2/home?#Instances).
1. Use stack output value of *Cloud9EnvironmentId* as filter to find the Cloud9 instance.
  ![Locate Cloud9 Instance](/images/locate-cloud9-instance.png)
1. Right click the instance, *Security* -> *Modify IAM Role*.
1. Choose the profile name matches to the *InstanceProfile* value from the stack output, and click *Apply*.
  ![Set Instance Role](/images/set-instance-role.png)

### Disable Cloud9 Managed Credentials
1. Launch [AWS Cloud9 Console](https://console.aws.amazon.com/cloud9/home?region=us-east-1#)
1. Locate the Cloud9 environment created for this lab and click "Open IDE". The environment title should start with *DevOpsGuruCloud9*.
1. At top menu of Cloud9 IDE, click *AWS Cloud9* and choose *Preferences*.
1. At left menu *AWS SETTINGS*, click *Credentials*.
1. Disable AWS managed temporary credentials:

    ![Disable Cloud 9 Managed Credentials](/images/disable-cloud9-credentials.png)

### Install prerequisite packages
Run commands below on Cloud9 Terminal to install prerequisite packages:

```
sudo yum install jq -y

export AWS_REGION=$(curl -s \
169.254.169.254/latest/dynamic/instance-identity/document | jq -r '.region')

sudo pip3 install requests
```
![Install Packages](/images/install-packages.png)

Clone the git repository to download the required CloudFormation templates:
```
git clone https://github.com/aws-samples/amazon-devopsguru-samples
cd amazon-devopsguru-samples/generate-devopsguru-insights/
```
### Deploy Serverless Infrastructure



## **Clean Up**


## **Survey**
Please help us to provide your feedback [here](https://amazonmr.au1.qualtrics.com/jfe/form/SV_0fhl0aCfOF1qjQO?Session=HOL05). Participants who complete the surveys from AWS Innovate Online Conference – Data and AI/ML Edition will receive a gift code for USD25 in AWS credits. AWS credits will be sent via email by 31 March, 2023.

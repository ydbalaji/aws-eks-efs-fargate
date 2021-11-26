# Getting started with Amazon EKS

This guide helps you to create all of the required resources to get started with Amazon Elastic Kubernetes Service (Amazon EKS) using eksctl, a simple command line utility for creating and managing Kubernetes clusters on Amazon EKS.

### Prerequisites 

*  An active AWS account

*  [kubectl](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html) – A command line tool for working with Kubernetes clusters. This guide requires that you use version 1.21 or later. For more information, see Installing kubectl.

*  [eksctl](https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html) – A command line tool for working with EKS clusters that automates many individual tasks. This guide requires that you use version 0.70.0 or later. For more information, see The eksctl command line utility.

*  [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html) – A command line tool for working with AWS services, including Amazon EKS. This guide requires that you use version 2.2.37 or later or 1.20.40 or later. 

*  [Docker](https://docs.docker.com/desktop/) - We will use Docker desktop application to create docker images.

*  [yq](https://stedolan.github.io/jq/download/) - is a lightweight and portable command-line YAML processor. yq uses jq like syntax but works with yaml files as well as json. 

*  Required IAM permissions – The IAM security principal that you're using must have permissions to work with Amazon EKS IAM roles and service linked roles, AWS CloudFormation, and a VPC and related resources

### Target technology stack

*  Amazon EFS
*  Amazon EKS
*  Fargate
*  Kubernetes

## Quick configuration with aws configure

For general use, the aws configure command is the fastest way to set up your AWS CLI installation\. When you enter this command, the AWS CLI prompts you for four pieces of information:
+ Access key ID
+ Secret access key
+ AWS Region
+ Output format

The AWS CLI stores this information in a *profile* \(a collection of settings\) named `default` in the `credentials` file\. By default, the information in this profile is used when you run an AWS CLI command that doesn't explicitly specify a profile to use\. For more information on the `credentials` file,

The following example shows sample values\. Replace them with your own values as described in the following sections\.

```
$ aws configure
AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
Default region name [None]: us-west-2
Default output format [None]: json
```

Let’s start by setting a few environment variables:

```
export AWS_REGION=us-east-1 
export CLUSTER_NAME=eksfgcluster
export AWS_ACCOUNT_ID=$(aws sts get-caller-identity --query 'Account' --output text)
export WOF_ACCOUNT_ID=$(aws sts get-caller-identity --query 'Account' --output text)
export WOF_AWS_REGION=$AWS_REGION
export WOF_EKS_CLUSTER=$CLUSTER_NAME
export STACK_NAME=eksctl-$CLUSTER_NAME-cluster
export ACCOUNT=$(aws sts get-caller-identity --query 'Account' --output text)
```

Steps:

*  [01 - Cluster creation](01-cluster)
*  [02 - ALB Ingress Controller](02-alb-controller)
*  [03 - Persistent storage(EFS)](03-persistent-storage)
*  [04 - Deployment(Drupal, Wordpress and MySQL)](04-deploy)
*  [05 - Examples](05-examples)


# Solution Architect

![aws elk fargate efs](images/aws-eks-fargate-efs.jpg) 
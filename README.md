
![alt text](https://miro.medium.com/max/2800/1*c_alK7iZgOyKMTCQBxpOBQ.png)


# AWS_EKS_Project


#                                          Description
## 1. Deploy a Kubernetes cluster in AWS EKS using Terraform.
## 2. Create Deployment for Prometheus and Grafana on EKS (using helm).


### Amazon Elastic Kubernetes Service (EKS) is a managed Kubernetes service that makes it easy for you to run Kubernetes on AWS without needing to install, operate, and maintain       your own Kubernetes control plane. Using Helm with Amazon EKS. The Helm package manager for Kubernetes helps you install and manage applications on your Kubernetes cluster. ... This topic helps you install and run the Helm binaries so that you can install and manage charts using the Helm CLI on your local system.


## Steps:

#### 1.Download the AWS CLI program, add it to path variables and configure it to use AWS using the command - aws configure --profile Admin. As terraform will also be using the same credentials for contacting AWS.

#### 2.Write terraform code for deploying a Kubernetes cluster on AWS using EKS.

#### 3.  Inside the cluster resource specify the name of the cluster, VPC inside which the cluster has to be launched, here I have used the ID's of the pre-created default subnet inside the default VPC. But you can also create your own VPC and subnets, define your own rules and use them.

#### 4. After the cluster, define the resource for the node groups - A node group is one or more Amazon EC2 instances that are deployed in an Amazon EC2 Auto Scaling group. All instances in a node group must:

##### Be the same instance type (When we use terraform code to deploy EKS cluster then by default t3.medium instance type is used, and I am using the same because prometheus needs at least this much to run using helm)
##### Be running the same Amazon Machine Image (AMI)
##### Use the same Amazon EKS worker node IAM role.
#### 5. Now go inside the directory where terraform code is present and run the commands
   ##### terraform commands are-:
      terraform init
      terraform apply --aprove


### Terraform code of cluster.yml-:
https://github.com/aniketambasta/AWS_EKS/blob/master/cluster.yml






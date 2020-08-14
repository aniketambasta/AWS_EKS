
![alt text](https://miro.medium.com/max/2800/1*c_alK7iZgOyKMTCQBxpOBQ.png)


# AWS_EKS


#                                          Description
## 1. Deploy a Kubernetes cluster in AWS EKS using Terraform.
## 2. Create Deployment for Prometheus and Grafana on EKS (using helm).


### Amazon Elastic Kubernetes Service (EKS) is a managed Kubernetes service that makes it easy for you to run Kubernetes on AWS without needing to install, operate, and maintain       your own Kubernetes control plane. Using Helm with Amazon EKS. The Helm package manager for Kubernetes helps you install and manage applications on your Kubernetes cluster. ... This topic helps you install and run the Helm binaries so that you can install and manage charts using the Helm CLI on your local system.


## Steps:

#### 1.Download the AWS CLI program, add it to path variables and configure it to use AWS using the command - aws configure --profile Admin. As terraform will also be using the same credentials for contacting AWS.

#### 2.Write terraform code for deploying a Kubernetes cluster on AWS using EKS.


### Terraform code of cluster.yml-:
https://github.com/aniketambasta/AWS_EKS/blob/master/cluster.yml






![alt text](https://miro.medium.com/max/2800/1*c_alK7iZgOyKMTCQBxpOBQ.png)


# AWS_EKS_Project


# task is to-:
## Deploy a Kubernetes cluster in AWS EKS using Terraform.


### What is AWS-EKS?

#### Amazon EKS (Elastic Container Service for Kubernetes) is a managed Kubernetes service that allows you to run Kubernetes on AWS without the hassle of managing the Kubernetes control plane.

#### Amazon EKS is also integrated with many AWS services to provide scalability and security for your applications, including the following:
Amazon **ECR** for container images

Elastic Load Balancing for load distribution

**IAM** for authentication

Amazon **VPC** for isolation

**Amazon Elastic File System (Amazon EFS)** provides a simple, scalable, fully managed elastic NFS file system for use with AWS Cloud services and on-premises resources.

### Pre-requisites:-

- AWS account
- AWS CLI configured in your device
- eksctl downloaded and path set
- kubectl downloaded and path set


### Benefits of EKS :

- High Availability
- Serverless option
- Secure
- Buid with the community


### How does Amazon EKS work?

- First, create an Amazon EKS cluster in the AWS Management Console or with the AWS CLI or one of the AWS SDKs.
- Then, launch worker nodes that register with the Amazon EKS cluster. We provide you with an AWS CloudFormation template that automatically configures your nodes.
- When your cluster is ready, you can configure your favorite Kubernetes tools (such as kubectl) to communicate with your cluster.
- Deploy and manage applications on your Amazon EKS cluster the same way that you would with any other Kubernetes environment.
![alt text](https://raw.githubusercontent.com/aniketambasta/AWS_EKS/master/ss1.png)
























### Amazon Elastic Kubernetes Service (EKS) is a managed Kubernetes service that makes it easy for you to run Kubernetes on AWS without needing to install, operate, and maintain       your own Kubernetes control plane.

## Steps:

#### 1.Download the AWS CLI program, add it to path variables and configure it to use AWS using the command - aws configure --profile Admin. As terraform will also be using the same credentials for contacting AWS.

#### 2.Write terraform code for deploying a Kubernetes cluster on AWS using EKS.

#### 3.  Inside the cluster resource specify the name of the cluster, VPC inside which the cluster has to be launched, here I have used the ID's of the pre-created default subnet inside the default VPC. But you can also create your own VPC and subnets, define your own rules and use them.

#### 4. After the cluster, define the resource for the node groups - A node group is one or more Amazon EC2 instances that are deployed in an Amazon EC2 Auto Scaling group. All instances in a node group must:

##### Be the same instance type (When we use terraform code to deploy EKS cluster then by default t3.medium instance type is used)
##### Be running the same Amazon Machine Image (AMI)
##### Use the same Amazon EKS worker node IAM role.
#### 5. Now go inside the directory where terraform code is present and run the commands
      terraform init
      terraform apply --aprove
      
##### You can see some services created which is required for cluster like security-groups, load balancer,volumes etc.

##### Now we have to update the config file of Kubernetes to use aws, so that we can use cluster from local system. use command for update file:      
      aws eks update-kubeconfig --name cluster-name


### Terraform code of cluster.yml-:
https://github.com/aniketambasta/AWS_EKS/blob/master/cluster.yml
### Terraform coe of deploy.yml-:
https://github.com/aniketambasta/AWS_EKS/blob/master/deploy.yml
### Terraform coe of pvc.yml-:
https://github.com/aniketambasta/AWS_EKS/blob/master/pvc.yml
### Terraform coe of sc.yml-:
https://github.com/aniketambasta/AWS_EKS/blob/master/sc.yml


### Few Screenshos of the task are-:

![alt text](https://github.com/aniketambasta/AWS_EKS/blob/master/dsa.PNG?raw=true)
![alt text](https://raw.githubusercontent.com/aniketambasta/AWS_EKS/master/asdfghjk.png)





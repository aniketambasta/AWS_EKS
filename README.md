

![alt text](https://miro.medium.com/max/2800/1*c_alK7iZgOyKMTCQBxpOBQ.png)


# AWS_EKS_Project


## Task is to-:
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
![alt text](https://github.com/aniketambasta/AWS_EKS_data/blob/master/ss1.png?raw=true)



### to create eks cluster
```
      apiVersion: eksctl.io/v1alpha5
      kind: ClusterConfig
      metadata:
        name: ekscluster
        region: ap-south-1
      nodeGroups:
        - name: ng1
          desiredCapacity: 2
          instanceType: t2.micro
          ssh:
            publicKeyName: aniket1234
        - name: ng2
          desiredCapacity: 2
          instanceType: t2.small
          ssh:
            publicKeyName: aniket1234
          ssh:
            publicKeyName: aniket1234
```
we have to run our cluster by running this command-:
```
      eksctl create cluster -f cluster.yml
   ```   
   
When the cluster has successfully created verify using given below command.
```
            ekstcl get cluster
   ```
now we have to Update the config file in .kube folder using the aws command.
```
aws eks update-kubeconfig --name clustername
   ```

### to create a mysql deployment
```
apiVersion: v1
kind: Service
metadata:
  name: mysql
  labels:
    app: wordpress
spec:
  ports:
    - port: 3306
  selector:
    app: wordpress
    tier: mysql
  clusterIP: None
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql
  labels:
    app: wordpress
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql
  labels:
    app: wordpress
spec:
  selector:
    matchLabels:
      app: wordpress
      tier: mysql
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: wordpress
        tier: mysql
    spec:
      containers:
      - image: mysql:5.6
        name: mysql
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-pass
              key: password
        ports:
        - containerPort: 3306
          name: mysql
        volumeMounts:
        - name: mysql-persistent-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-persistent-storage
        persistentVolumeClaim:
          claimName: mysql
```

### to create wordpress deployment
```
apiVersion: v1
kind: Service
metadata:
  name: wordpress
  labels:
    app: wordpress
spec:
  ports:
    - port: 80
  selector:
    app: wordpress
    tier: frontend
  type: LoadBalancer
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: wp
  labels:
    app: wordpress
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: wordpress
  labels:
    app: wordpress
spec:
  selector:
    matchLabels:
      app: wordpress
      tier: frontend
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: wordpress
        tier: frontend
    spec:
      containers:
      - image: wordpress:4.8-apache
        name: wordpress
        env:
        - name: WORDPRESS_DB_HOST
          value: wordpress-mysql
        - name: WORDPRESS_DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-pass
              key: password
        ports:
        - containerPort: 80
          name: wordpress
        volumeMounts:
        - name: wordpress-persistent-storage
          mountPath: /var/www/html
      volumes:
      - name: wordpress-persistent-storage
        persistentVolumeClaim:
          claimName: wp
```

Now we will create a **kustomization** file.
```
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
secretGenerator:
  - name: mysql-pass
    literals:
        - password=redhat
resources:
  - mysql.yml
  - wordpress.yml
```

Now run the file using given command, this command will execute the **kustomization.yml** file 
```
kubectl create -k .   
```









  
          
          
Now run the below command to get **LoadBalancer Ip** , EKS uses external loadbalancer that also make pods public to outside world so run the command given below.
```
kubectl get all       
   ```
Copy the LoadBalancer Ip and paste in the browser and get access to deployed Application over EKS Cluster.


## install aws CLI
![alt text](https://github.com/aniketambasta/AWS_EKS_data/blob/master/ss11.png?raw=true)


## to create IAM user with administrator access
![alt text](https://github.com/aniketambasta/AWS_EKS_data/blob/master/ss10.png?raw=true)


   


      
      
## Few ScreenShots of the tasks are-:
![alt text](https://github.com/aniketambasta/AWS_EKS_data/blob/master/ss2.PNG?raw=true)

![alt text](https://github.com/aniketambasta/AWS_EKS_data/blob/master/ss4.png?raw=true)

![alt text](https://github.com/aniketambasta/AWS_EKS_data/blob/master/ss3.png?raw=true)

![alt text](https://github.com/aniketambasta/AWS_EKS_data/blob/master/ss5.png?raw=true)

![alt text](https://github.com/aniketambasta/AWS_EKS_data/blob/master/ss6.png?raw=true)

![alt text](https://github.com/aniketambasta/AWS_EKS_data/blob/master/ss7.png?raw=true)

![alt text](https://github.com/aniketambasta/AWS_EKS_data/blob/master/ss8.png?raw=true)

![alt text](https://github.com/aniketambasta/AWS_EKS_data/blob/master/ss9.png?raw=true)
      
      
      
      

 ###  Terraform code of [cluster.yml](https://github.com/aniketambasta/AWS_EKS_data/blob/master/cluster.yml)
### Terraform coe of [wordpress.yml](https://github.com/aniketambasta/AWS_EKS_data/blob/master/wordpress.yml)
### Terraform coe of [mysql.yml](https://github.com/aniketambasta/AWS_EKS_data/blob/master/mysql.yml)
### Terraform coe of [kustomization.yml](https://github.com/aniketambasta/AWS_EKS_data/blob/master/kustomization.yml)
        
      
      
      
      
      
      
      
      












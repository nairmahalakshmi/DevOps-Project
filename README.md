# DevOps- Project
This project uses an Employee Management System built on SpringBoot as the base project to be integrated with DevOps tool. 

# Database 
The application uses a database implemented using PostgreSQL. 
1) An EC2 instance was created to host the database server installing and configuring PostgreSQL and enabling the necessary ports for communication with the server.
2) An EBS volume was attached to the EC2 instance and then mounted to it 
3) A cronjob is created to automate backups.

# Maven 
1) The application was packaged into a .jar file using Maven and a docker image of the .jar file was build by writing a Dockerfile.
2) The docker image was then pushed to DockerHub so that it can be deployed within the Kubernetes cluster. 

# Kubernetes Cluster 
1) A Kubernetes cluster consisting of a single master and 2 slave nodes was constructed using EKS. The necessary dependencies were installed as per the Kubernetes official documentation.
2) Once the connection between the master and slave nodes were established, a deployment object was created having 2 replicas by pulling the image from DockerHub and a service object was created to enable access to the application running in the pods.
3) A target group containing the slave nodes was created and an application load balancer was linked to it to balance the traffic between the nodes.
4) The application was accessed through the DNS of the load balancer- http://clusteralb-1649197627.ap-south-1.elb.amazonaws.com/

# Jenkins Pipeline
A Jenkins pipeline was created for CI/CD automation consisting of the following steps:
1) Source Code Management: Jenkins was connected to Git to clone the repository.
2) Build and Packaging: Maven is used as the build tool to build and package the application into a .jar file.
3) Containerization: Docker image of the application is build and pushed to DockerHub.
4) Deployment: Dockerized application is deployed to Tomcat server.

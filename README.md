# DevOps-Project
This project uses an Employee Management System built on SpringBoot as the base project to be integrated with DevOps tool. 

The application uses a database implemented using PostgreSQL. An EC2 instance was created to host the database server installing and configuring PostgreSQL and enabling the necessary ports for communication with the server.
An EBS volume was attached to the EC2 instance and then mounted to it and a cronjob is created to run everyday.

The application was packaged to a .jar file using Maven and a docker image of the .jar file was build by writing a Dockerfile and the docker image was then pushed to DockerHub so that it can be deployed within the Kubernetes cluster. 

A Kubernetes cluster consisting of a single master and 2 slave nodes was constructed using 3 EC2 instances. The necessary dependencies were installed as per the Kubernetes official documentation.
Once the connection between the master and slave nodes were established, a deployment object was created having 2 replicas by pulling the image from DockerHub and a service object was created to enable ??.
A target group containing the slave nodes was created and an application load balancer was linked to it to balance the traffic between the nodes.
The application was accessed through the DND of the load balancer.

A Jenkins pipeline was created for CI/CD automation consisting of the following steps:
1) Source Code Management: Jenkins was connected to Git to clone the repository.
2) Build and Packaging: Maven is used as the build tool to build and package the application into a .jar file.
3) SonarQube integration: The code quality is analyzed by the static code analyzer and reports are generated.
4) Containerization: Docker image of the application is build and pushed to DockerHub.
5) Deployment: Dockerized application is deployed to Tomcat server.

pipeline {
    agent any
    tools {
        maven "Maven3"
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/nairmahalakshmi/DevOps-Project.git'
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Image Build') {
            steps {
                sh "docker build -t mahalakshminair/devops:latest ."
            }
        }
        stage('Login to DockerHub'){
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push Image') {
            steps {
                sh "docker push mahalakshminair/devops:latest"
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh "docker run -p 8000:8080 -d mahalakshminair/devops:latest"
                }
            }
        }
    }
}

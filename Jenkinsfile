pipeline {
    agent {
        label 'agent1'
    }
    tools {
        maven "MAVEN_HOME"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'githubcredentials', url: 'https://github.com/j-rin/java_sql.git'
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Scan') {
            steps {
                withSonarQubeEnv(installationName: 'sonar-server') { 
                sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Image Build') {
            steps {
                script{
                sh "whoami"
                sh "docker build -t jerinpaul/jenkins-app:latest ."
                }
            }
        }
        stage('push to dockerhub') {
            steps {
                script{
                sh "docker login"
                sh "docker push jerinpaul/jenkins-app:latest"
                }
            }
        }
        stage('Deploying to K8s') {
            steps {
                withKubeConfig([credentialsId: 'kubernetescredentials', serverUrl: 'https://77CA947B7DE0FEE8F24A92959D3C387F.gr7.ap-south-1.eks.amazonaws.com']) {
                    sh 'kubectl apply -f deployment.yaml'
                    sh 'kubectl get pods'
                }
            }
        } 
    }      
}

pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sainadh30/Python-Webapp.git'
            }
        }
        stage('Docker Build') {
            steps {
                sh "make image"
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: '83176aa2-6f6b-49ae-b457-a3725b716f65', toolName: 'docker') {
                        sh "make push"
                    }
                }  
            }
        }
        stage('Docker deploy') {
            steps {
                script {
                    withDockerRegistry(credentialsId: '83176aa2-6f6b-49ae-b457-a3725b716f65', toolName: 'docker') {
                        sh "docker images"
                        sh "docker run -d -it --rm -p 5000:5000 sai3009/python-webapp:latest"
                    }
                }
            }
        }
    }
}

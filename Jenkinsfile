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
                    withDockerRegistry(credentialsId: 'f4017afd-4fc7-4021-83c2-6447d4aaa9d7', toolName: 'docker') {
                        sh "make push"
                    }
                }  
            }
        }
        stage('Docker deploy') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'f4017afd-4fc7-4021-83c2-6447d4aaa9d7', toolName: 'docker') {
                        sh "docker images"
                        sh "docker run -d -it --rm -p 5000:5000 sai3009/python-webapp:latest"
                    }
                }
            }
        }
    }
}

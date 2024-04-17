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
                    withDockerRegistry(credentialsId: '0028c087-a650-4df3-8696-836ce2be5650', toolName: 'docker') {
                        sh "make push"
                    }
                }  
            }
        }
        stage('Docker deploy') {
            steps {
                script {
                    withDockerRegistry(credentialsId: '0028c087-a650-4df3-8696-836ce2be5650', toolName: 'docker') {
                        sh "docker images"
                        sh "docker run -d -it --rm -p 5000:5000 sai3009/python-webapp:latest"
                    }
                }
            }
        }
    }
}

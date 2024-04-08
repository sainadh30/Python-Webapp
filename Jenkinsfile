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
                script{
                    withDockerRegistry(credentialsId: '245f8c88-61f5-4eeb-b048-0ba48440ee23', toolName: 'docker') {
                        sh "make push"
                    }
                }
            }
        }
        stage('Docker deploy') {
            steps {
                script{
                    withDockerRegistry(credentialsId: '245f8c88-61f5-4eeb-b048-0ba48440ee23', toolName: 'docker') {
                         sh "docker images”        
                         sh "docker run -d -it --rm -p 5000:5000 sainadh/python-webapp:latest"

                    }
                }
            }
        }
       
    }
}


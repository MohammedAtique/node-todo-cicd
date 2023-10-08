pipeline {
    agent { label "aws-agent" }
    
    stages {
        
        stage('code') {
            steps {
                git url: "https://github.com/MohammedAtique/node-todo-cicd", branch: "master"
            }
        }
        stage('build and test') {
            steps {
                sh 'docker build . -t mohammedatique/node-todo-app:latest'
            }
        }
        stage('Login and push image') {
            steps {
                echo "Login into docker hub and pushing image"
                
                withCredentials([usernamePassword('credentialsId':'dockerHub','passwordVariable':'dockerHubPassword','usernameVariable':'dockerHubUsername')]) {
                    sh 'docker login -u $dockerHubUsername -p $dockerHubPassword'
                    sh 'docker push mohammedatique/node-todo-app:latest'
                }
            }
        }
        stage('deploy') {
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}

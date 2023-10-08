pipeline {
    agent any  
    stages {
        stage('Code') {
            steps {
                git url: "https://github.com/MohammedAtique/node-todo-cicd.git", branch: "master"
            }
        }
        stage('Build & Test') {
            steps {
                 sh "docker build . -t node-todo-app"
            }
        }
        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'node-todo-demo-app', passwordVariable: 'pass', usernameVariable: 'user')]) {
        	        sh "docker login -u ${env.user} -p ${env.pass}"
        	        sh "docker tag node-todo-app ${env.user}/node-todo-app:latest"
        	        sh "docker push ${env.user}/node-todo-app:latest"
                }
            }
        }
        stage('Deploy') {
            steps {
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}

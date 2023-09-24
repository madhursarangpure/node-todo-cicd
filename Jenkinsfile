pipeline {
    agent { label 'dev-agent' }
    stages {
        stage('Code') {
            steps {
                script {
                    properties([pipelineTriggers([pollSCM('')])])
                }
                git url: 'https://github.com/madhursarangpure/node-todo-cicd.git', branch: 'master'    
            }
            
        }
        stage('Code Build') {
            steps {
                sh 'docker build . -t 8871255273/node-todo-app-cicd:latest' 
            }
            
        }
        stage('Login and push image') {
            steps {
                echo "login into dockerHub and pushing image.."
                withCredentials([usernamePassword(credentialsId:'dockerhub',passwordVariable:'dockerHubPassword',usernameVariable:'dockerHubUsername')]){
                    sh "docker login -u ${env.dockerHubUsername} -p ${env.dockerHubPassword}" 
                    sh "docker push 8871255273/node-todo-app-cicd:latest"
                }
            }
            
        }
        stage('Code test') {
            steps {
                echo "Code testing...!"    
            }
            
        }
        stage('Code Deploy') {
            steps {
                sh 'docker-compose down && docker-compose up -d'    
            }
            
        }
    }
}

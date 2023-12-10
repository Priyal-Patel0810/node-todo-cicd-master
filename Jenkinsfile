pipeline {
    agent any

    stages{
        stage('Build Maven'){
            steps{
                git url: "https://github.com/Priyal-Patel0810/node-todo-cicd-master.git", branch: "master"
                echo 'bhaiyya code clone ho gaya'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t node-app-todo .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                   sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                   sh "docker tag node-app-test-new:latest ${env.dockerHubUser}/node-app-test-new:latest"
                   sh "docker push ${env.dockerHubUser}/node-app-test-new:latest"}
                }
            }
        }
        stage('Deploy'){
            steps{
                script{
                    sh "docker-compose down && docker-compose up -d"
                    echo 'deployment ho gayi'
                }
            }
        }
    }
}

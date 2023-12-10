pipeline {
    agent any
    tools{
        maven 'Maven 3.9.6'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Priyal-Patel0810/node-todo-cicd-master.git']]])
                sh 'mvn clean install'
                echo 'Building of maven project is completed'
            }
        }
        stage("build and test"){
            steps{
                sh "docker build -t node-app-test-new ."
                echo 'Image is built'
            }
        }
        stage("scan image"){
            steps{
                echo 'image scanning is completed'
            }
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag node-app-test-new:latest ${env.dockerHubUser}/node-app-test-new:latest"
                sh "docker push ${env.dockerHubUser}/node-app-todo:latest"
                echo 'Pushing image is completed'
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'Deployment Completed'
            }
        }
    }
}

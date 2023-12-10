pipeline {
    agent any
    tools{
        maven 'maven_3_5_0'
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
                docker build . -t node-app-todo
                docker run -d --name node-app-container -p 8000:8000 node-app-todo
                echo 'Image is built'
            }
        }
        stage("scan image"){
                                                                                                                           1,10          Top                echo 'image scanning is completed'
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

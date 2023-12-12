pipeline {
    agent any
    
    stages{
        stage('Build Maven'){
            steps{
                def tool= tool 'maven'
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Priyal-Patel0810/node-todo-cicd-master']])
                sh 'mvn clean install'
                
                echo 'Maven Project build is created'
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
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u priyal0810 -p ${dockerhubpwd}'

                    sh 'docker push priyal0810/node-app-todo'
                }  
            }
        }
    }
        stage('Deploy'){
            steps{
                script{
                        sh "docker-compose down && docker-compose up -d"
                        echo 'Deployment is completed'
                }
            }
        }
    }
}

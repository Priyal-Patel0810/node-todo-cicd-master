pipeline {
    agent any
    
    stages{
        stage('Build Project'){
            steps{
                git url: "https://github.com/Priyal-Patel0810/node-todo-cicd-master.git", branch: "master"
                echo 'Project is build'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t node-app-todo .'
                    echo 'Image is created'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u priyal0810 -p ${dockerhubpwd}'
                    sh 'docker push priyal0810/node-app-todo:latest'
                    echo 'Image is pushed to Docker Hub'
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

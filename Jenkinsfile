pipeline {
    agent any

    stages{
        stage('Build Maven'){
            steps{
                git url: "https://github.com/Priyal-Patel0810/node-todo-cicd-master.git", branch: "master"
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
                        ssh -i /Downloads/DevOps-keypair.pem ubuntu@172.31.20.115
                        docker pull priyal0810/node-app-todo:latest
                        docker run -d -p 8000:8000 priyal0810/node-app-todo:latest
                }
            }
        }
    }
}

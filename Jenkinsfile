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
                    sh "docker -H ssh://jenkins@http://3.89.252.63/ run -d -p 8000:8080 priyal0810/node-app-todo"
                }
            }
        }
    }
}

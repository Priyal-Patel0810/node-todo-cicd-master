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
                        sshCommand remote: "ec2-user@${172.31.20.115}", command: '''
                        # Pull the latest Docker image
                        docker pull $priyal0810/node-app-todo

                        # Stop and remove the existing container
                        docker stop node-app-todo || true
                        docker rm node-app-todo || true

                        # Run the new container
                        docker run -d --name node-app-todo -p 8000:8000 $DOCKER_IMAGE
                }
            }
        }
    }
}

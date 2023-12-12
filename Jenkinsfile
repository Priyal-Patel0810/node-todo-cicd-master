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
                        sshagent(credentials: ['18.213.4.84']) {
                       
                        name = 'EC2Instance'
                        host = '172.31.25.28'
                        user = 'ubuntu'
                        identityFile = '/Downloads/Devops.pem'

                        // Pull the Docker image
                        command="docker pull priyal0810/node-app-todo:latest"
                        run()

                        // Run the Docker container
                        command="docker run -d -p 8000:8000 priyal0810/node-app-todo:latest"
                        run()
                      
                        echo 'Deployment is completed'
                }
            }
        }
    }
}
}

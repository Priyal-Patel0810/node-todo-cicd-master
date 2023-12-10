pipeline {
    agent any
    tools{
        maven 'maven_3_6_3'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Priyal-Patel0810/node-todo-cicd-master.git']]])
                sh 'mvn clean install'
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
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u priyal0810 -p ${dockerhubpwd}'

}
                   sh 'docker push priyal0810/node-app-todo'
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

pipeline {
    environment {
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
    agent any
    tools {
    nodejs 'nodejs'
}
    stages {
        stage('Git Clone'){
            steps {
                echo 'Cloning Git Repo'
                git 'https://github.com/pranaypiyush25/Node.js-Hello-World-Microservice-Example.git'
            }
        }
        stage('Install dependencies'){
            steps{
                echo 'started npm install'
                sh 'npm install'
            }
        }
        stage('Test'){
            steps{
                sh 'npm test'
            }
        }
        stage('version'){
            steps{
                sh 'docker --version'
            }
        }
        stage('Docker Build'){
            steps{
                script{
                  dockerImage = docker.build registry + ":$BUILD_NUMBER"
            }
        }
        stage('Deploy Image') {
          steps{
             script {
                docker.withRegistry('https://registry.hub.docker.com', registryCredential ) {
                dockerImage.push("${env.BUILD_NUMBER}")            
                dockerImage.push("latest")  
              }
            }
          }
        }
      }
    }
}

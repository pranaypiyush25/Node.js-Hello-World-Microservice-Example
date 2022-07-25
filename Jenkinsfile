pipeline {
    environment {
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
    agent any
    tools {
    nodejs 'nodejs'
    docker 'docker'
}
    stages {
        stage('Git Clone') {
            steps {
                echo 'Cloning Git Repo'
                git 'https://github.com/pranaypiyush25/Node.js-Hello-World-Microservice-Example.git'
            }
        }
        stage('Installing npm'){
            steps{
                echo 'started npm install'
                sh 'npm install'
            }
        }
        stage('test')
        {
            steps{
                sh 'npm test'
            }
        }
        stage('version')
        {
            steps{
                sh 'docker --version'
            }
        }
        stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
      }
    }
}

pipeline {
    environment {
    registry = "palakollu145/helloworld"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
    agent any
    tools {
    nodejs 'nodejs'
}
    stages {
        stage('git') {
            steps {
                echo 'cloning git'
                git credentialsId: '79504c40-37cf-484b-8f23-4e27b24a6721', url: 'https://github.com/pranaypiyush25/Node.js-Hello-World-Microservice-Example'
            }
        }
        stage('install npm'){
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
        stage('Initialize') {
        steps{
            script{
                def dockerHome = tool 'docker'
                env.PATH = "${dockerHome}/bin:${env.PATH}"
            }
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

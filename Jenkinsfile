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
        stage('git') {
            steps {
                echo 'cloning git'
                git 'https://github.com/pranaypiyush25/Node.js-Hello-World-Microservice-Example.git'
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

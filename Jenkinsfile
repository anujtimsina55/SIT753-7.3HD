pipeline {
  agent any

  environment {
    DOCKER_IMAGE = "smart-meal-planner"
  }

  stages {
    stage('Build') {
      steps {
        echo 'Building Docker image...'
        bat 'docker build -t %DOCKER_IMAGE% .'
      }
    }

    stage('Test') {
      steps {
        echo 'Installing deps and running tests...'
        bat 'npm ci --prefix server'
        bat 'npm test --prefix server'
      }
    }
  }
}

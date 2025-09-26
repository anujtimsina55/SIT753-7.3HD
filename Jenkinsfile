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

    stage('Code Quality') {
      steps {
        echo 'Running SonarCloud analysis...'
        withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
          bat '''
            npx sonar-scanner ^
              -Dsonar.projectKey=anujtimsina55_SIT753-7.3HD ^
              -Dsonar.organization=anujtimsina55 ^
              -Dsonar.host.url=https://sonarcloud.io ^
              -Dsonar.login=%SONAR_TOKEN%
          '''
        }
      }
}
  }
}

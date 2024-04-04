pipeline {
  agent any
  stages {
    stage('clone') {
      steps {
        git url: 'https://github.com/spring-projects/spring-petclinic.git', branch: 'main'
      }
    }

    stage('build') {
      steps {
        sh 'mvn package'
      }
    }

    stage('sonar') {
      steps {
        withSonarQubeEnv('sonarqube_sever') {
                sh 'mvn clean package sonar:sonar'
        }
      }
    }
  }
}


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
         script{
           def scannerHome= tool 'mikey_sonar';
        withSonarQubeEnv('sonarqube_server') {
                 sh "${scannerHome}/bin/sonar-scanner \
                      -Dsonar.projectKey=pet-clinic \
                       -Dsonar.java.binaries=target/classes"
        }
      }
    }
  }

    stage('sonar2') {
      steps {
        script{
          def scannerHome= tool 'mikey_sonar';
        withSonarQubeEnv('sonarcloud_server') {
                sh "${scannerHome}/bin/sonar-scanner \
                      -Dsonar.projectKey=mikey1 \
                      -Dsonar.organization=mikey1 \
                       -Dsonar.java.binaries=target/classes"
        }
        }
      }
    }
}
}

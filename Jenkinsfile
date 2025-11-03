pipeline {
  agent any

  tools {
    maven 'maveone'
    jdk 'JDK21'
  }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build & Test') {
      steps {
        script {
          if (isUnix()) {
            sh 'mvn -B -DskipTests=false clean install'
          } else {
            // Windows agents use 'bat'
            bat 'mvn -B -DskipTests=false clean install'
          }
        }
      }
    }
  }

  post {
    always {
      junit '**/target/surefire-reports/*.xml'
      archiveArtifacts artifacts: '**/target/*.jar', allowEmptyArchive: true
    }
  }
}

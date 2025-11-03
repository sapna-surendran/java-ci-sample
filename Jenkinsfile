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
        sh 'mvn -B -DskipTests=false clean install'
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

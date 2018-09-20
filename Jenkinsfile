pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        sh './mvnw clean package'
      }
    }
    stage('Archive') {
      steps {
        archiveArtifacts 'target/deploy-tomcat.war'
      }
    }
  }
}

pipeline {
  agent any

  parameters {
    string(name: 'TOMCAT_URL', defaultValue: 'http://localhost:8080/manager/text', description: '')
    string(name: 'TOMCAT_SERVER', defaultValue: 'target-tomcat', description: '')
  }

  stages {
    stage('Build') {
      steps {
        sh './mvnw clean package'
        sh """
          ./mvnw org.apache.tomcat.maven:tomcat7-maven-plugin:deploy \
          -Dmaven.tomcat.url=${params.TOMCAT_URL} \
          -Dmaven.tomcat.server=${params.TOMCAT_SERVER} \
          -Dmaven.tomcat.update=true
        """
      }
    }
    stage('Archive') {
      steps {
        archiveArtifacts 'target/deploy-tomcat.war'
      }
    }
  }
}

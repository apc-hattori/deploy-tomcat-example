pipeline {
  agent any

  parameters {
    string(name: 'TOMCAT_URL', defaultValue: env.TOMCAT_URL, description: 'デプロイ先Tomcat ManagerのURL\n例. http://localhost:8080/manager/text')
    string(
      name: 'TOMCAT_URLS',
      defaultValue: 'http://localhost:8080/manager/text',
      description: 'デプロイ先Tomcat ManagerのURL一覧\nカンマ(,)区切りで複数指定できる\n例. http://localhost:8080/manager/text,http://localhost:8081/manager/text',
    )
    string(name: 'TOMCAT_SERVER', defaultValue: 'target-tomcat', description: 'settings.xml上に書かれたデプロイに使用する認証情報のID')
  }

  stages {
    stage('Build') {
      steps {
        sh './mvnw clean package'
        sh """
          ./mvnw org.apache.tomcat.maven:tomcat7-maven-plugin:deploy-only \
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

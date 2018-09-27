pipeline {
  agent any

  parameters {
    string(
      name: 'TOMCAT_URLS',
      defaultValue: env.TOMCAT_URLS,
      description: 'デプロイ先Tomcat ManagerのURL一覧\nカンマ(,)区切りで複数指定できる\n例. http://localhost:8080/manager/text,http://localhost:8081/manager/text',
    )
    string(name: 'TOMCAT_SERVER', defaultValue: 'target-tomcat', description: 'settings.xml上に書かれたデプロイに使用する認証情報のID')
  }

  stages {
    stage('Build') {
      steps {
        sh './mvnw clean package'
      }
    }
    stage('Deploy') {
      steps {
        script {
          def urls = params.TOMCAT_URLS.split(',')
          def configs = [:]
          urls.eachWithIndex { url, index ->
            def u = url
            configs["server-${index}"] = {
              sh """
                ./mvnw org.apache.tomcat.maven:tomcat7-maven-plugin:deploy-only \
                -Dmaven.tomcat.url=${u} \
                -Dmaven.tomcat.server=${params.TOMCAT_SERVER} \
                -Dmaven.tomcat.update=true
              """
            }
          }
          parallel(configs)
        }
      }
    }
    stage('Archive') {
      steps {
        archiveArtifacts 'target/deploy-tomcat.war'
      }
    }
  }
}

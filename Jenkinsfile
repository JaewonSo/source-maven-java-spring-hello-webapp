pipeline {
     agent {
      label "jenkins-node"
    }

  triggers {
  //  pollSCM('* * * * *')
  githubPush()
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', 
        url: 'https://github.com/JaewonSo/source-maven-java-spring-hello-webapp.git'
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean package -DskipTests=true'
      }
    }
    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }
    stage('Deploy') {
      steps {
        deploy adapters: [tomcat9(credentialsId: 'tomcat-manger', url: 'http://43.201.42.179:8080')], contextPath: null, war: 'target/hello-world.war'
      }
    }
  }
}
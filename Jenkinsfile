pipeline {
  agent any
  
  stages {
    stage('Build') {
      steps {
        withEnv(["JAVA_HOME=/opt/jdk-18", "MAVEN_HOME=/usr/share/maven"]) { 
          sh "${env.JAVA_HOME}/bin/java -version"
          sh "${env.MAVEN_HOME}/bin/mvn --version"
          sh 'mvn clean install'
          sh 'sudo docker build -t my-java-app .'
        }
      }
    }
    
    stage('Deploy') {
      steps {
        sh 'sudo docker run -d -p 8080:8080 my-java-app'
      }
    }
  }
}

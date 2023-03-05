pipeline {
  agent any
  
  stages {
    stage('Build') {
      steps {
        sh 'docker stop my-java-app || true'
        withEnv(["JAVA_HOME=/opt/jdk-18", "MAVEN_HOME=/usr/share/maven"]) { 
          sh "${env.JAVA_HOME}/bin/java -version"
          sh "${env.MAVEN_HOME}/bin/mvn --version"
          sh 'mvn clean install -DskipTests'
          sh 'docker build -t my-java-app .'
        }
      }
    }  
    stage('Deploy') {
      steps {
        sh 'docker stop my-java-app || true && docker rm my-java-app || true'
        sh 'docker run -d -p 8080:8080 --name my-java-app my-java-app'
      }
    }
  }
}

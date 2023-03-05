pipeline {
  agent any
  
  stages {
    stage('Build') {
      steps {
        withEnv(["JAVA_HOME=/opt/jdk-18", "MAVEN_HOME=/mnt/c/Program Files/apache-maven-3.8.7"]) { 
          sh "${env.JAVA_HOME}/bin/java -version"
          sh "${env.MAVEN_HOME}/bin/mvn --version"
          sh 'mvn clean install'
          sh 'docker build -t my-java-app .'
        }
      }
    }
    
    stage('Deploy') {
      steps {
        sh 'docker run -d -p 8080:8080 my-java-app'
      }
    }
  }
}

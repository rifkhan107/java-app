pipeline {
  agent any
  
  stages {
    stage('Build') {
      steps {
        withEnv(["JAVA_HOME=/opt/jdk-18", "MAVEN_HOME=/usr/share/maven"]) { 
          sh "${env.JAVA_HOME}/bin/java -version"
          sh "${env.MAVEN_HOME}/bin/mvn --version"
          sh 'mvn clean install'
          sh 'docker build -t my-java-app .'
        }
      }
    }
    
    stage('Stop Docker Container') {
      steps {
        script {
          try {
            sh 'docker stop $(docker ps -q --filter ancestor=my-java-app:latest || true)'
          } catch (error) {
            echo "Error Stoping Docker Conatiner ${error}"
          }
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

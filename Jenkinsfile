pipeline {
  agent any

  stages {
    stage('Build and Test') {
      steps {
       withEnv(["JAVA_HOME=/opt/jdk-18", "MAVEN_HOME=/usr/share/maven"]) {  
        sh "${env.JAVA_HOME}/bin/java -version"
        sh "${env.MAVEN_HOME}/bin/mvn --version"
        sh 'mvn clean install -DskipTests'
       }
      }
    }

  stages {
    stage('Build') {
      steps {
        sh 'mvn clean install'
        sh 'docker build -t my-java-app .'
      }
    }
    stage('Deploy') {
      steps {
        sh 'docker run -d -p 8080:8080 my-java-app'
      }
    }
  }
}
}

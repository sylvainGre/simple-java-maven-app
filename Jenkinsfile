pipeline {
  agent {
    docker {
      image 'maven:3-alpine'
      args '-v /root/.m2:/root/.m2 '
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }

    stage('Deploy') {
      steps {
        sh 'ssh admin@reta-app.fr'
        sh 'scp /var/jenkins_home/workspace/simple-java-maven-app_master/target/my-app-1.0-SNAPSHOT.jar admin@reta-app.fr:/docker/openjdk-docker/src/production/app'
      }
    }

  }
}
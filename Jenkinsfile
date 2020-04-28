pipeline {
  agent none
  stages {
    stage('Build') {
      agent {
        docker {
          image 'maven:3-alpine'
          args '-v /root/.m2:/root/.m2 -v /var/jenkins_home/workspace/target:/target_build/'
        }

      }
      steps {
        sh 'mvn -B -DskipTests clean package'
        sh 'cp /var/jenkins_home/workspace/simple-java-maven-app_master/target/my-app-1.0-SNAPSHOT.jar /target_build/'
      }
    }

    stage('Deploy') {
      agent any
      steps {
        sh '''scp /var/jenkins_home/workspace/target/* admin@reta-app.fr:/docker/openjdk-docker/src/production/app/
 '''
      }
    }

  }
}
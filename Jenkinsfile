pipeline {
  agent any
  stages {
    stage('Build') {
      //when { not { branch 'master' } }
      steps {
        echo './gradlew clean build'
      }
    }
    stage('Quality Analysis') {
      //when { not { branch 'master' } }
      parallel {
        stage ('Unit Test') {
          agent any
          steps {
            echo './gradlew test'
          }
        }
        stage('Sonar Scan') {
          steps {
            echo 'Publicando reportes a Sonar'
          }
        }
      }
    }
    stage('Containerization & Push') {
      //when { branch 'develop' }
      steps {
        echo "foo"
      }
      post {
        success {
          echo 'Image Container Registry successful'
          slackSend(channel: "jenkins-updates", message: "Image Container Registry successful")
        }
        failure {
          echo 'Image Build failure'
        }
      }
    }
    
  }
}

def message = 'Hola'

def slackResponse = slackSend(channel: "jenkins-updates", message: "Empezando construcción del trabajo ${JOB_URL}")

pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        slackSend(channel: slackResponse.threadId, message: "Construyendo....")
      }
    }
    stage('Quality Analysis') {
      parallel {
        stage ('Unit Test') {
          agent any
          steps {
            slackSend(channel: slackResponse.threadId, message: "Testing....")
          }
        }
        stage('Sonar Scan') {
          steps {
            slackSend(channel: slackResponse.threadId, message: "Reportando a Sonar....")
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
          slackSend(channel: slackResponse.threadId, color: 'good', message: "Image Container Registry successful")
          slackSend(channel: slackResponse.threadId, color: 'bad', message: "Mensaje 'Bad'")
          slackSend(channel: slackResponse.threadId, color: 'warning', message: "Mensaje 'Warning'")
          slackSend(channel: slackResponse.threadId, color: '#FF33E9', message: "Mensaje en Rosa?")
          slackSend(channel: slackResponse.threadId, color: '#333CFF', message: "Mensaje en Azul?")
          slackSend(channel: slackResponse.threadId, color: '#ff0000', message: "Un posible error")
          
        }
        failure {
          echo 'Image Build failure'
          slackSend(channel: slackResponse.threadId, color: 'Error', message: "Image Container Registry successful")
        }
      }
    }
    
  }
}

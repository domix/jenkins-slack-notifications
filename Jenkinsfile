def message = 'Hola'
def channel = 'jenkins-updates'

def slackResponse = slackSend(channel: channel, message: "Empezando construcción del trabajo ${JOB_URL}")

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
          slackSend(channel: channel, color: 'good', message: "Image Container Registry successful")
          slackSend(channel: channel, color: 'bad', message: "Mensaje 'Bad'")
          slackSend(channel: channel, color: 'warning', message: "Mensaje 'Warning'")
          slackSend(channel: channel, color: '#FF33E9', message: "Mensaje en Rosa?")
          slackSend(channel: channel, color: '#333CFF', message: "Mensaje en Azul?")
          slackSend(channel: channel, color: '#ff0000', message: "Un posible error")
          
        }
        failure {
          echo 'Image Build failure'
          slackSend(channel: channel, color: '#ff0000', message: "Image Container Registry successful")
        }
      }
    }
    
  }
}

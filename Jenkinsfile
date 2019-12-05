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
        //def slackResponse = slackSend(channel: "jenkins-updates", message: "Here is the primary message")
        //slackSend(channel: slackResponse.threadId, message: "Thread reply #1")
        //slackSend(channel: slackResponse.threadId, message: "Thread reply #2")
      }
      post {
        success {
          /*def blocks = [
            [
              "type": "section",
              "text": [
                "type": "mrkdwn",
                "text": "Hello, Assistant to the Regional Manager Dwight! *Michael Scott* wants to know where you'd like to take the Paper Company investors to dinner tonight.\n\n *Please select a restaurant:*"
              ]
            ],
            [
              "type": "divider"
            ],
            [
              "type": "section",
              "text": [
                "type": "mrkdwn",
                "text": "*Farmhouse Thai Cuisine*\n:star::star::star::star: 1528 reviews\n They do have some vegan options, like the roti and curry, plus they have a ton of salad stuff and noodles can be ordered without meat!! They have something for everyone here"
              ],
              "accessory": [
                "type": "image",
                "image_url": "https://s3-media3.fl.yelpcdn.com/bphoto/c7ed05m9lC2EmA3Aruue7A/o.jpg",
                "alt_text": "alt text for image"
              ]
            ]
          ]*/

          echo 'Image Container Registry successful'
          slackSend(channel: "jenkins-updates", blocks: [
            [
              "type": "section",
              "text": [
                "type": "mrkdwn",
                "text": "Hello, Assistant to the Regional Manager Dwight! *Michael Scott* wants to know where you'd like to take the Paper Company investors to dinner tonight.\n\n *Please select a restaurant:*"
              ]
            ],
            [
              "type": "divider"
            ],
            [
              "type": "section",
              "text": [
                "type": "mrkdwn",
                "text": "*Farmhouse Thai Cuisine*\n:star::star::star::star: 1528 reviews\n They do have some vegan options, like the roti and curry, plus they have a ton of salad stuff and noodles can be ordered without meat!! They have something for everyone here"
              ],
              "accessory": [
                "type": "image",
                "image_url": "https://s3-media3.fl.yelpcdn.com/bphoto/c7ed05m9lC2EmA3Aruue7A/o.jpg",
                "alt_text": "alt text for image"
              ]
            ]
          ])
          
        }
        failure {
          echo 'Image Build failure'
        }
      }
    }
    
  }
}

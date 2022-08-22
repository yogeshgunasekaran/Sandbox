pipeline {
    agent any

    stages {
        stage('Intro') {
            steps {
                echo 'This project is to integrate GitHub, Jenkins & Telegram'
            }
        }

    stage('Clean workspace') {
        steps {
               cleanWs()
        }
      }
      stage('Checkout') {
        steps {
               checkout scm: [$class: 'GitSCM', userRemoteConfigs: [[url: 'https://github.com/yogeshgunasekaran/Sandbox.git']], branches: [[name: 'origin/main']]], poll: false
        }
      }
      stage('Deploy web-app') {
        steps {
                sh 'sudo cp -r /var/lib/jenkins/workspace/GitHub_Jenkins_Telegram_Integration/* /var/www/html/ '
        }
      }
      stage('Notification') {
         
        steps {
            script{
                    withCredentials([string(credentialsId: ‘telegramToken’, variable: ‘TOKEN’),
                    string(credentialsId: ‘telegramChatId’, variable: ‘CHAT_ID’)]) {
                    telegramSend(messsage:”test message”,chatId:${CHAT_ID})
                    }
                  }
                }  

            }
        
    }
    
}

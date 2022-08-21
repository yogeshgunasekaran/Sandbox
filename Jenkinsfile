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
                sh 'cp -r /var/lib/jenkins/workspace/GitHub_Jenkins_Telegram_Integration/* /var/www/html/ '
        }
      }
    }
    
}

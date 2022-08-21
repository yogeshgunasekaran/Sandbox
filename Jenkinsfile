pipeline {
    agent any

    stages {
        stage('Intro') {
            steps {
                echo 'This project is to integrate GitHub, Jenkins & Telegram'
            }
        }
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

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
               script {
                        withCredentials([string(credentialsId: 'telegramToken', variable: 'TOKEN'),
                             string(credentialsId: 'telegramChatId', variable: 'CHAT_ID')]) {
                                sh """
                                          curl -s -X POST https://api.telegram.org/bot${TOKEN}/sendMessage -d chat_id=${CHAT_ID} -d parse_mode="HTML" -d text="<b>Project</b> : POC \
                                              <b>Branch</b>: main \
                                               <b>Build </b> : OK \
                                               <b>Test suite</b> = Passed"
                                """
                        }
                    }    
                }
            }
      when:
      status: [success, failure]
      format: markdown
      message: 
      {{#success build.status}}
      ✅ Build #{{build.number}} of `{{repo.name}}` succeeded.

      📝 Commit by {{commit.author}} on `{{commit.branch}}`:

      ```
      {{commit.message}}
      ```

      🌐 {{ build.link }}
      {{else}}
      ❌ Build #{{build.number}} of `{{repo.name}}` failed.

      📝 Commit by {{commit.author}} on `{{commit.branch}}`:

      ```
      {{commit.message}}
      ```

      🌐 {{ build.link }}
      {{/success}}
    }
    
}

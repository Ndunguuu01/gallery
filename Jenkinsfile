pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                
                git url: 'https://github.com/ndunguuu01/gallery.git', branch: 'master'
            }
        }
        stage('Install Dependencies') {
            steps {
                
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                
                sh 'npm run build' 
            }
        }
        stage('Deploy to Heroku') 
            steps {
                
                sh 'git push heroku master' 
            }
        }
        stage('Test') {
            steps {

                sh 'npm test'
            }
        }

    }

    post {
        success {
            slackSend (
                channel: "${env.SLACK_CHANNEL}",
                color: 'good',
                message: "Build #${env.BUILD_NUMBER} - Success! View it here: ${env.BUILD_URL}"
            )
        }
        failure {
            slackSend (
                channel: "${env.SLACK_CHANNEL}",
                color: 'danger',
                message: "Build #${env.BUILD_NUMBER} - FAILED! Check it out: ${env.BUILD_URL}"
            )
        }
    }

}


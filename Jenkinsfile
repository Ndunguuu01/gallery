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
        stage('Deploy to Herku') 
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
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }

    post {
    failure {
        mail to: bndungu061@gmail.com,
             subject: "Build Failed: ${env.BUILD_ID}",
             body: "Something went wrong. Please check the Jenkins console output for details."
    }
}

}


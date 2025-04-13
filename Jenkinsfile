pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo 'Cloning repo...'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-static-site .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8082:80 my-static-site'
            }
        }
    }

    post {
        success {
            sh '''
                curl -X POST -H 'Content-Type: application/json' \
                -d '{"text":"✅ Jenkins build succeeded!"}' \
                'https://chat.googleapis.com/v1/spaces/your-webhook-here'
            '''
        }
        failure {
            sh '''
                curl -X POST -H 'Content-Type: application/json' \
                -d '{"text":"❌ Jenkins build failed!"}' \
                'https://chat.googleapis.com/v1/spaces/AAQA6T-eab0/messages?key=AIzaSyDdI0hCZtE6vySjMm-WEfRq3CPzqKqqsHI&token=FomwqNQ1EieiUyZZ3mZwDqjHiVGlnOcX1vhQWAq42bU'
            '''
        }
    }
}


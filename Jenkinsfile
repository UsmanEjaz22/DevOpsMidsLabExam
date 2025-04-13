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
}

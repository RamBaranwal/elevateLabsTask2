pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building application...'
                bat 'docker build -t jenkins-cicd-app .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application...'
                bat 'docker run --rm jenkins-cicd-app nginx -t'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'

                bat '''
                    docker stop jenkins-cicd-app
                    docker rm jenkins-cicd-app
                    docker run -d --name jenkins-cicd-app -p 8081:80 jenkins-cicd-app
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'CI/CD Pipeline failed!'
        }
    }
}
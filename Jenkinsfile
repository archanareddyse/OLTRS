
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                bat 'mvn -version'
                bat 'mvn clean package'
            }
        }

        stage('Archive WAR') {
            steps {
                archiveArtifacts artifacts: 'target/*.war',
                                 allowEmptyArchive: false
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker --version'
                bat 'docker build -t oltrs:latest .'
            }
        }
    }

    post {
        success {
            echo 'OLTRS CI pipeline completed successfully!'
        }
        failure {
            echo 'Build failed. Check Console Output.'
        }
    }
}

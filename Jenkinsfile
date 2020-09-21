pipeline {
    agent {
        docker {
            image 'node:6-alpine' 
            args '-p 3333:3333' 
        }
    }
    
    environment {
        CI = 'true'
    }

    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello world!"'
                sh 'npm install' 
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}

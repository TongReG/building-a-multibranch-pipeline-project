pipeline {
    agent {
        docker {
            image 'node:6-alpine' 
            args '-p 3333:3333 -p 5000:5000' 
        }
    }
    
    environment {
        CI = 'true'
    }

    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello Building React Apps!"'
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
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deploy-for-production.sh'
                input message: 'Finished serving the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}

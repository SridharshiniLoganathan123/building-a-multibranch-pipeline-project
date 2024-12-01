pipeline {
    agent any
    environment {
        CI='true'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Running npm install...'
                bat 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Running test script...'
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" ./jenkins/scripts/test.sh'
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development'
            }
            steps {
                echo 'Delivering for development...'
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" ./jenkins/scripts/deliver-for-development.sh'
                timeout(time: 5, unit: 'MINUTES') {
                    input message: 'Finished using the web site? (Click "Proceed" to continue)'
                }
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" ./jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'
            }
            steps {
                echo 'Deploying for production...'
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" ./jenkins/scripts/deploy-for-production.sh'
                timeout(time: 5, unit: 'MINUTES') {
                    input message: 'Finished using the web site? (Click "Proceed" to continue)'
                }
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" ./jenkins/scripts/kill.sh'
            }
        }
    }
}
pipeline {
    agent any
    environment {
        CI = 'true' 
    }
    stages {
        stage('Build') {
            steps {
                bat 'npm install'
            }
        }
        stage('Test') {
            steps {
                // Added debug echo for clarity
                bat 'echo Running test script'
                // Corrected path and escaped quotes
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" -c "./jenkins/scripts/test.sh"'            
                }
        }
    }
}
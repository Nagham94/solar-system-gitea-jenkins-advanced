pipeline {
    agent any

    tools {
       nodejs 'nodejs-23.7.0'
    } 
    stages {
        stage('version check') {
            steps {
                sh '''
                    node -v
                    npm -v
                '''
            }
        }
        stage('Installing Dependencies') {
            steps {
                sh 'npm install --no-audit'
            }
        }
    }  
}  
       
 

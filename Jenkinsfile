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
    }  // Missing closing brace added here
}  // This was missing

       

       
 

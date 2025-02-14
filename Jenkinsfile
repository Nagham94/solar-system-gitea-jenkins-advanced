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
        stage('Dependency Scanning') {
            parallel {
                    stage('NPM Dependency Audit') {
                        steps {
                          sh '''
                            npm audit --audit-level=critical
                            echo $?
                           '''
                        }
                    }
                    stage('OWASP Dependency Check') {
                        steps {
                          dependencyCheck additionalArguments: '''
                            --scan \'./\' 
                            --out \'./\'  
                            --format \'ALL\' 
                            --disableYarnAudit \
                            --prettyPrint''', odcInstallation: 'owasp-depcheck-10'

                          dependencyCheckPublisher failedTotalCritical: 1, pattern: 'dependency-check-report.xml', stopBuild: false
                       }
                    }
            }
        }
    }  
}  

       
 

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
                    npm install mongoose@6.13.5
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

                          publishHTML([allowMissing: true, alwaysLinkToLastBuild: true, keepAll: true, reportDir: './', reportFiles: 'dependency-check-jenkins.html', reportName: 'dependency check HTML Report', reportTitles: '', useWrapperFileDirectly: true])

                          junit allowEmptyResults: true, keepProperties: true, stdioRetention: '', testResults: 'dependency-check-junit.xml'  
                       }
                    }
            }
        }
    }  
}  

       
 

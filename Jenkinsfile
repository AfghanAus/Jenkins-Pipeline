pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building with Maven'
                
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Testing with JUnit'
                
            }
            post {
                failure {  
                        // Send email with the log file attached
                        archiveArtifacts artifacts: '**/target/*.log', allowEmptyArchive: true
                        mail to: 'wahidhashimiadler2018@gmail.com',
                             subject: currentBuild.result,
                             body: "Test Failed"
                             attachmentspattern: '**/target/*.log'       
                    }
                success{
                    archiveArtifacts artifacts: '**/target/*.log', allowEmptyArchive:
                    mail to:'wahidhashimiadler2018@gmail.com',
                    subject: currentBuild.result,
                    body: "Test was successfull"
                    attachmentspattern: '**/target/*.log'
                    }
                }
        }
        
        
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code using sonar-scanner'
                
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan using OWASP Dependency-Check'
            }
            post {
                failure {  
                        // Send email with the log file attached
                        archiveArtifacts artifacts: '**/target/*.log', allowEmptyArchive:
                        mail to: 'wahidhashimiadler2018@gmail.com',
                             subject: currentBuild.result,
                             body: "Scan Failed"
                             attachmentspattern: '**/target/*.log'
                             
                    }
                success{
                    archiveArtifacts artifacts: '**/target/*.log', allowEmptyArchive:
                    mail to:'wahidhashimiadler2018@gmail.com',
                    subject: currentBuild.result,
                    body: "Scan was successfull"
                    attachmentspattern: '**/target/*.log'
                    }
                }
            
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging with SCP'
                
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging with JUnit'
                // Example integration tests on staging
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production with AWS EC2 server'
                
            }
        }
        stage('Building') {
            steps {
                echo 'Building'
                
            }
        }
        
    }
}

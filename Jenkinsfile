pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean package' // Example using Maven
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                sh 'mvn test' // Example using Maven for unit tests
                sh 'mvn verify' // Example for integration tests
            }
            post {
                always {
                    script {
                        // Save logs to a file
                        def logFile = "unit_integration_tests.log"
                        writeFile file: logFile, text: currentBuild.rawBuild.getLog(1000).join("\n")
                        
                        // Send email with the log file attached
                        mail to: 'wahidhashimiadler2018@gmail.com',
                             subject: "Jenkins Pipeline: Unit and Integration Tests - ${currentBuild.currentResult}",
                             body: "The Unit and Integration Tests stage has ${currentBuild.currentResult}.\nCheck console output at ${env.BUILD_URL}.",
                             attachmentsPattern: logFile
                    }
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo 'Analyzing the code...'
                sh 'sonar-scanner' // Example using SonarQube
            }
        }
        
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                sh 'npm audit' // Example using npm audit or OWASP Dependency-Check
            }
            post {
                always {
                    script {
                        // Save logs to a file
                        def logFile = "security_scan.log"
                        writeFile file: logFile, text: currentBuild.rawBuild.getLog(1000).join("\n")
                        
                        // Send email with the log file attached
                        mail to: 'wahidhashimiadler2018@gmail.com',
                             subject: "Jenkins Pipeline: Security Scan - ${currentBuild.currentResult}",
                             body: "The Security Scan stage has ${currentBuild.currentResult}.\nCheck console output at ${env.BUILD_URL}.",
                             attachmentsPattern: logFile
                    }
                }
            }
        }
        
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                sh 'scp target/app.war user@staging-server:/path/to/deploy/' // Example using SCP
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Example integration tests on staging
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                sh 'scp target/app.war user@production-server:/path/to/deploy/' // Example using SCP
            }
        }
    }
}

pipeline {
    agent any
    
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Fetching the source code from the directory path specified by the environment variable.'
                echo 'Compiling the code and generating any necessary artifacts.'
                sh 'mvn clean package' // Assuming Maven is used for the build
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests.'
                sh 'mvn test'
                echo 'Running integration tests.'
                sh 'mvn verify'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Checking the quality of the code using a code analysis tool.'
                sh 'sonar-scanner' // Assuming SonarQube is used for code analysis
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Identifying vulnerabilities using a security scanning tool.'
                sh 'npm audit' // Assuming npm audit or a similar tool is used for security scanning
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on the staging environment.'
                // Add your specific commands for staging environment integration tests
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying the code to the production environment.'
                // Add your specific commands for deployment
            }
        }
    }
    
    post {
        always {
            script {
                def logFile = "build-log-${env.BUILD_NUMBER}.txt"
                def logZip = "build-log-${env.BUILD_NUMBER}.zip"
                
                // Save build logs to a file
                writeFile file: logFile, text: currentBuild.rawBuild.getLog().join("\n")
                
                // Compress the log file
                sh "zip ${logZip} ${logFile}"
                
                // Send email with the compressed log file attached
                emailext(
                    to: 'youremail@example.com',
                    subject: "Jenkins Pipeline: Build ${currentBuild.fullDisplayName} - ${currentBuild.currentResult}",
                    body: "The build has completed with status: ${currentBuild.currentResult}.\nCheck console output at ${env.BUILD_URL}.",
                    attachmentsPattern: logZip
                )
                
                // Clean up the log file and the zip
                sh "rm ${logFile} ${logZip}"
            }
        }
    }
}

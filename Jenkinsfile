pipeline {
    agent any
    environment {
        LOG_DIR = "${WORKSPACE}/logs"
        EMAIL_RECIPIENT = 'adelalghamdis2@gmail.com'
    }
    stages {
        stage('Setup') {
            steps {
                script {
                    sh 'mkdir -p ${LOG_DIR}'
                    echo 'Setup complete.'
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    echo 'Building the project with Maven.'
                    echo 'Tool used: Maven'
                    sh "echo 'Maven build simulated.' > ${LOG_DIR}/build.log"
                }
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests using JUnit.'
                    echo 'Tools used: JUnit'
                    sh "echo 'JUnit tests simulated.' > ${LOG_DIR}/test.log"
                }
            }
        }
        stage('Code Analysis') {
            steps {
                script {
                    echo 'Analyzing code quality with SonarQube.'
                    echo 'Tool used: SonarQube'
                    sh "echo 'SonarQube analysis simulated.' > ${LOG_DIR}/code_analysis.log"
                }
            }
        }
        stage('Security Scan') {
            steps {
                script {
                    echo 'Performing security scan with OWASP ZAP.'
                    echo 'Tool used: OWASP ZAP'
                    sh "echo 'OWASP ZAP security scan simulated.' > ${LOG_DIR}/security_scan.log"
                }
            }
        }
        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to AWS EC2 staging environment.'
                    sh "echo 'Deployment to staging .' > ${LOG_DIR}/staging_deployment.log"
                }
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests in the staging environment.'
                    sh "echo 'Integration tests on staging .' > ${LOG_DIR}/staging_tests.log"
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to AWS EC2 production environment.'
                    sh "echo 'Deployment to production .' > ${LOG_DIR}/production_deployment.log"
                }
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'logs/*'
        }
        success {
            script {
                sendEmail("${LOG_DIR}", "Pipeline execution completed successfully.")
            }
        }
        failure {
            script {
                sendEmail("${LOG_DIR}", "Pipeline execution failed. Check logs for details.")
            }
        }
    }
}

def sendEmail(String logDir, String emailBody) {
    def buildLogs = sh(script: "cat ${logDir}/build.log", returnStdout: true).trim()
    def testLogs = sh(script: "cat ${logDir}/test.log", returnStdout: true).trim()
    def securityLogs = sh(script: "cat ${logDir}/security_scan.log", returnStdout: true).trim()
    def codeAnalysisLogs = sh(script: "cat ${logDir}/code_analysis.log", returnStdout: true).trim()
    def stagingDeploymentLogs = sh(script: "cat ${logDir}/staging_deployment.log", returnStdout: true).trim()
    def stagingTestsLogs = sh(script: "cat ${logDir}/staging_tests.log", returnStdout: true).trim()
    def productionDeploymentLogs = sh(script: "cat ${logDir}/production_deployment.log", returnStdout: true).trim()

    mail to: EMAIL_RECIPIENT,
         subject: "Pipeline Notification: ${currentBuild.currentResult}",
         body: """\
            ${emailBody}\n\n\
            Build Logs:\n${buildLogs}\n\n\
            Test Logs:\n${testLogs}\n\n\
            Security Scan Logs:\n${securityLogs}\n\n\
            Code Analysis Logs:\n${codeAnalysisLogs}\n\n\
            Staging Deployment Logs:\n${stagingDeploymentLogs}\n\n\
            Staging Tests Logs:\n${stagingTestsLogs}\n\n\
            Production Deployment Logs:\n${productionDeploymentLogs}
         """
}

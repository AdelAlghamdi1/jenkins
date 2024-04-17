pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the project with Maven.'
                echo 'Tool used: Maven'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using JUnit.'
                echo 'Tools used: JUnit'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing code quality with SonarQube.'
                echo 'Tool used: SonarQube'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing security scan with OWASP ZAP.'
                echo 'Tool used: OWASP ZAP'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to AWS EC2 staging environment.'
                echo 'Deployment tool: AWS CLI or Jenkins EC2 plugin'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests in the staging environment.'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to AWS EC2 production environment.'
            }
        }
    }
    post {
        success {
            mail to: 'adelalghamdis2@gmail.com',
                 subject: "Build Successful Email",
                 body: " build was successful Thanks."
        }
    }
}

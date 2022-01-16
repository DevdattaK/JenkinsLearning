pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                powershell 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('Deploy to staging') {
            steps {
                build job: 'deploy-to-staging'
            }
        }

        stage('Deploy to PRODUCTION') {
            steps {
                timeout(time: 5, unit: 'DAYS') {
                    input message: 'Approve PRODUCTION deployment?'
                }

                build job: 'deploy-to-production'
            }

            post {
                success {
                    echo 'Deployment to PROD is a success.'
                }
                failure {
                    echo 'Deployment to PROD failed.'
                }
            }
        }
    }
}
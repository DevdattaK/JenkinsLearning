pipeline{
    agent any

    stages {
        stage ('Build'){
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

        stage('Deploy to staging'){
            steps{
                build job: 'deploy-to-staging'
            }
        }
    }
}
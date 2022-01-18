pipeline {
    agent any

    parameters {
        string(name: 'tomcat_staging', defaultValue: '3.83.116.236', description: 'Staging Server')
        string(name: 'tomcat_production', defaultValue: '35.175.174.111', description: 'Production Server')
    }

    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('Build') {
            steps {
                powershell 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('Deployments'){
            parallel{
                stage('Deploy to staging'){
                    steps{
                        bat "winscp -i D:\\PersonalDevelopment\\Programming\\Workspaces\\maven-project\\SSHKey\\keyPair.pem **/target/*.war ec2-user@${params.tomcat_staging}:/var/lib/tomcat/webapps"
                    }
                }
                stage('Deploy to production'){
                    steps {
                        bat "winscp -i D:\\PersonalDevelopment\\Programming\\Workspaces\\maven-project\\SSHKey\\keyPair.pem **/target/*.war ec2-user@${params.tomcat_production}:/var/lib/tomcat/webapps"
                    }
                }
            }
        }
    }
}
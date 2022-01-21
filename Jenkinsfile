pipeline{
    agent any

    stages {
        stage('Build'){
            steps{
                powershell "mvn clean package"
                powershell "docker build . -t tomcatwebapp:${env.BUILD_ID}"
            }
        }
    }
}
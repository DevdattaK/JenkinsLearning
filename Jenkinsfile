pipeline{
    agent any

    stages {
        stage('Build'){
            steps{
                powershell "mvn clean package"
            }
        }
    }
}
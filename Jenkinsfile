pipeline {
    agent{
        label "slave"
    }
    stages{
        stage("Git Checkout"){
            steps{
                git branch: 'main', url: 'https://github.com/gerarahul/sample--project.git'
            }
        }
        stage("Unit Testing"){
            steps{
                sh "mvn test"
            }
        }
        stage("Integration testing"){
            steps{
                sh 'mvn verify -DskipUnitTests'
            }
        }
        stage('Maven Build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('Static code analysis'){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'Sonar-api-key'){
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
    }
}
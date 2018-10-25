pipeline{
    agent any
    stages{
        stage('Build counterwebapp'){
            steps{
                bat 'mvn clean install'
            }
            post{
                success{
                    archiveArtifacts artifacts : '**/*.war'
                }
            }
        }
        stage('Build w1'){
            steps{
                build job : 'w1'
            }
        }
        stage('Build w2'){
            steps{
                build job : 'w2'
            }
        }
        stage('Build w3'){
            steps{
                build job : 'w3'
            }
        }
    }
}
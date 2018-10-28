pipeline{
    agent any
	tools {
        maven 'localMaven'
    }
    stages{
        stage('Build counterwebapp'){
            steps{
                sh 'mvn clean install'
            }
            post{
                success{
                    archiveArtifacts artifacts : '**/*.war'
                }
            }
        }
        stage('Deploy to Staging'){
            steps{
                build job : 'Staging_Env'
            }
        }
        stage('Deploy to Production'){
            steps{
				timeout (time: 5, unit:'DAYS'){
                    input message: 'Approve PRODUCTION Deployment?'
                }
                build job : 'Prod_Env'
            }
			post{
                success{
                    echo 'Deployment on PRODUCTION is Successful'
                }

                failure{
                    echo 'Deployement Failure on PRODUCTION'
                }
            }
        }
    }
}
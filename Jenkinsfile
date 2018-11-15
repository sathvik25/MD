pipeline{
    agent any
    stages{
        stage('Build counterwebapp'){
			tools {
				maven 'Maven'
			}
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
                build job : 'Staging_Env_New'
            }
        }
        stage('Deploy to UAT'){
            steps{
				timeout (time: 5, unit:'DAYS'){
                    input message: 'Approve UAT Deployment?'
                }
                build job : 'UAT_Env_New'
            }
			post{
                success{
                    echo 'Deployment on UAT is Successful'
                }

                failure{
                    echo 'Deployement Failure on UAT'
                }
            }
        }
		stage('Deploy to Production'){
            steps{
				timeout (time: 5, unit:'DAYS'){
                    input message: 'Approve Production Deployment?'
                }
                build job : 'Prod_Env_New'
            }
			post{
                success{
                    echo 'Deployment on Production is Successful'
                }

                failure{
                    echo 'Deployement Failure on Production'
                }
            }
        }
		
    }
}
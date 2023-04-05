@Library('my-shared-lib') _

pipeline {
    agent any

parameters{

        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/Destroy')
}

    stages{
	
        stage('Code Checkout'){
	when { expression {  params.action == 'create' } }
            steps{
            gitCheckout(
                url: "https://github.com/Bhanu-Ganga-DevOPs/Jenkins-Shared-Docker-Multistagee.git"

            )
            }
        }
        stage('UNIT TEST'){
	when { expression {  params.action == 'create' } }

            steps{
                script{
                    mvnTest()
                }
            }
        }

	stage('Intergration Test'){
        when { expression {  params.action == 'create' } }        
   
	 steps{
                script{
                    mvnIntegrationTest()
                }
            }
        }
    	stage('Static Code Analysis'){
	    when { expression {  params.action == 'create' } }
            steps{
                script{
                    def sonarQubecredentialsId = 'sonarqube-api'
                    staticCodeAnalysis(sonarQubecredentialsId)
                }
            }
        }
        
    }
}

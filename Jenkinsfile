@Library('my-shared-lib') _

pipeline {
    agent any

parameters{

        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/Destroy')
        string(name: 'Imagename', description: 'name of the docker build', defaultValue: 'javapp')
        string(name: 'ImageTag', description: 'tag of the docker build', defaultValue: 'javapp')
        string(name: 'AppName', description: 'name of the Application', defaultValue: 'sprintboot')
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

        stage('Quality gate status check : Sonarqube'){
	    when { expression {  params.action == 'create' } }
            steps{
                script{
                    def sonarQubecredentialsId = 'sonarqube-api'
                    qualityGateStatus(sonarQubecredentialsId)
                }
            }
        }

        stage('Maven Build'){
	    when { expression {  params.action == 'create' } }
            steps{
                script{
                    
                    mvnBuild()
                }
            }
        }

        stage('Docker image Build'){
	    when { expression {  params.action == 'create' } }
            steps{
                script{
                    
                    mvnBuild("${params.Imagename}","${params.ImageTag}","${params.AppName}")
                }
            }
        }
        
    }
}

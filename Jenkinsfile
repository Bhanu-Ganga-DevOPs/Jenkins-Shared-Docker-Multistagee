// Include the shared lib into the jenkins file.
@Library('my-shared-lib') _



//Declarative pipeline
pipeline {
    agent any

parameters{
        // action is a variable to make our pipeline parameterized - user controlable
        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/Destroy')
        string(name: 'ImageName', description: "name of the docker build", defaultValue: 'javapp')
        string(name: 'ImageTag', description: "tag of the docker build", defaultValue: 'v1')
        string(name: 'DockerHubUser', description: "name of the Application", defaultValue: 'bhanuayikam')
}

    stages{
	
        stage('Code Checkout'){
        // Checkout the code when the action is create - selected by user
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

	    stage('Integration Test'){
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
        stage('Docker Image Build : DockerHub '){
         when { expression {  params.action == 'create' } }
            steps{
               script{

                   dockerBuild("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
               }
            }
        }

        stage('Docker Image Scan : Trivy '){
         when { expression {  params.action == 'create' } }
            steps{
               script{

                   dockerImageScan("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
               }
            }
        }

        stage('Docker Image Push : DockerHub '){
         when { expression {  params.action == 'create' } }
            steps{
               script{

                   dockerImagePush("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
               }
            }
        }

        stage('Docker Image Cleanup : DockerHub '){
         when { expression {  params.action == 'create' } }
            steps{
               script{

                   dockerImageCleanup("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
               }
            }
        }
    }
}

@Library('my-shared-lib') _

pipeline {
    agent any

}


    stages{
	
        stage('Code Checkout'){
#	when { expression { param.action == 'create'}}
            steps{
            gitCheckout(
                url: "https://github.com/Bhanu-Ganga-DevOPs/Jenkins-Shared-Docker-Multistagee.git"

            )
            }
        }
        stage('UNIT TEST'){


            steps{
                script{
                    mvnTest()
                }
            }
        }

	stage('Intergration Test'){


            steps{
                script{
                    mvnIntegrationTest()
                }
            }
        }
    	stage('Static Code Analysis'){


            steps{
                script{
                    staticCodeAnalysis()
                }
            }
        }
        
    }
}

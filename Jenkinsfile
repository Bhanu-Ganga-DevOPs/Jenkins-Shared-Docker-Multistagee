@Library('my-shared-lib') _

pipeline {
    agent any

    parameters{
        choice(name: 'action',choice: 'create/ndestroy', description:'Choose create/destroy')
    }


    stages{
	
        stage('Code Checkout'){
	when { expression { param.action == 'create'}}
            steps{
            gitCheckout(
                url: "https://github.com/Bhanu-Ganga-DevOPs/Jenkins-Shared-Docker-Multistagee.git"

            )
            }
        }
        stage('UNIT TEST'){

	when { expression { param.action == 'create'}}
            steps{
                script{
                    mvnTest()
                }
            }
        }

	stage('Intergration Test'){

	when { expression { param.action == 'create'}}
            steps{
                script{
                    mvnIntegrationTest()
                }
            }
        }
    	stage('Static Code Analysis'){

	    when { expression { param.action == 'create'}}
            steps{
                script{
                    staticCodeAnalysis()
                }
            }
        }
        
    }
}

@Library('my-shared-lib') _

pipeline {
    agent any
    stages{
        stage('Code Checkout'){

            steps{
            gitCheckout(
                url: "https://github.com/Bhanu-Ganga-DevOPs/Jenkins-Shared-Docker-Multistagee.git"

            )
            }
        }

        stage('unit testing'){
            
            step{
                script{
                    mvnTest()
                }
            }

        }
    }
}
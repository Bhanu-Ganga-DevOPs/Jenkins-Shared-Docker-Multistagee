@Library('my-shared-lib') _

pipeline {
    agent any
    stages{
        stage('Code Checkout'){

            steps{
            gitCheckout(
                credentialsId: "git_creds",
                url: "https://github.com/Bhanu-Ganga-DevOPs/Jenkins-Shared-Docker-Multistagee.git"
            )
            }
        }
    }
}
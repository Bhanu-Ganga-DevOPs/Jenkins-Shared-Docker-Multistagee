pipeline {
    agent any
    stages{
        stage('Code Checkout'){

            steps{
                    git credentialsId: 'git_creds', url: 'https://github.com/Bhanu-Ganga-DevOPs/Jenkins-Shared-Docker-Multistagee.git'
            }
        }
    }
}
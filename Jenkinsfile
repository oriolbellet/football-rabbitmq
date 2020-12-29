pipeline {

    environment {
        PROJECT_ID = 'football-299420'
        CLUSTER_NAME = 'football-cluster'
        LOCATION = 'europe-west1-b'
        CREDENTIALS_ID = 'football'
        GIT_SHA = sh(returnStdout: true, script: 'git rev-parse HEAD').trim().take(6)
    }

    agent any

    stages {

        stage('Deploy to GKE') {
            when { branch 'master' }
            steps{
                step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'deployment.yml', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
            }
        }
       
    }
    post {
        always {
           cleanWs()
        }
    }
    
}

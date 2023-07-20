pipeline {
    agent any
    environment {
        PROJECT_ID = credentials('simpleweb_gke_projectID')
        CLUSTER_NAME = credentials('simpleweb_gke_clusterName')
        LOCATION = credentials('simpleweb_gke_location')
        CREDENTIALS_ID = credentials('simpleweb_gke_credentialsID')
    }
    stages { 
        stage('SCM') {
            steps {
                script {
                    checkout scm
                }
            }
        }
        stage('Deploy to GKE') {
                    steps{
                        step([
                        $class: 'KubernetesEngineBuilder',
                        projectId: env.PROJECT_ID,
                        clusterName: env.CLUSTER_NAME,
                        location: env.LOCATION,
                        manifestPattern: 'deploy_efrei/all',
                        credentialsId: env.CREDENTIALS_ID,
                        namespace: 'pacman',
                        verifyDeployments: true])
                    }
        }
    }
}

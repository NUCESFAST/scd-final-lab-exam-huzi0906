pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'i211187'
                
                // Checkout the code from the GitHub repository
                git 'https://github.com/NUCESFAST/scd-final-lab-exam-huzi0906.git'
            }
        }

        stage('Build Docker images') {
            steps {
                echo 'i211187'
                
                // Use docker compose to build images
                sh 'docker compose build'
            }
        }

        stage('Push Docker images') {
            steps {
                echo 'i211187'

                // Login to Docker Hub
                withCredentials([usernamePassword(credentialsId: 'dockerHubCredentials', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
                    sh 'echo $DOCKER_HUB_PASSWORD | docker login -u $DOCKER_HUB_USERNAME --password-stdin'
                }

                // Tag and push the Docker images
                sh 'docker tag scd-final-lab-exam-huzi0906-client:latest huzi0906/scd-final-lab-exam-huzi0906-client:latest'
                sh 'docker push huzi0906/scd-final-lab-exam-huzi0906-client:latest'

                sh 'docker tag scd-final-lab-exam-huzi0906-server_post:latest huzi0906/scd-final-lab-exam-huzi0906-server_post:latest'
                sh 'docker push huzi0906/scd-final-lab-exam-huzi0906-server_post:latest'

                sh 'docker tag scd-final-lab-exam-huzi0906-server_auth:latest huzi0906/scd-final-lab-exam-huzi0906-server_auth:latest'
                sh 'docker push huzi0906/scd-final-lab-exam-huzi0906-server_auth:latest'

                sh 'docker tag scd-final-lab-exam-huzi0906-server_classrooms:latest huzi0906/scd-final-lab-exam-huzi0906-server_classrooms:latest'
                sh 'docker push huzi0906/scd-final-lab-exam-huzi0906-server_classrooms:latest'

                sh 'docker tag scd-final-lab-exam-huzi0906-server_event_bus:latest huzi0906/scd-final-lab-exam-huzi0906-server_event_bus:latest'
                sh 'docker push huzi0906/scd-final-lab-exam-huzi0906-server_event_bus:latest'
            }
        }           
    }
}
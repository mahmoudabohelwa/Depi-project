pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/mahmoudabohelwa/Depi-project', branch: 'main'
            }
        }

        stage('Build and Push Frontend') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKERPASS', usernameVariable: 'DOCKERNAME')]) {
                    sh """
                    docker build -t mahmoudabohelwa3474/frontend:latest ./frontend
                    docker login -u ${DOCKERNAME} -p ${DOCKERPASS}
                    docker push mahmoudabohelwa3474/frontend:latest
                    """
                }
            }
        }

        stage('Build and Push Backend') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKERPASS', usernameVariable: 'DOCKERNAME')]) {
                    sh """
                    docker build -t mahmoudabohelwa3474/backend:latest ./backend
                    docker login -u ${DOCKERNAME} -p ${DOCKERPASS}
                    docker push mahmoudabohelwa3474/backend:latest
                    """
                }
            }
        }

        stage('Terraform Destroy and Apply') {
            steps {
                dir('terraform') { 
                    sh """
                    terraform init
                    terraform destroy -auto-approve
                    terraform apply -auto-approve -var-file=(...............)
                    """
                }
            }
        }
    }
}

pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/your-username/your-repo.git', branch: 'main'
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

        stage('Deploy with Docker Compose') {
            steps {
                sh """
                docker-compose -f /home/mahmoud/depi/docker-compose.yml
                docker-compose -f /home/mahmoud/depi/docker-compose.yml up -d --remove-orphans
                """
            }
        }
    }
}

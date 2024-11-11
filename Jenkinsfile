pipeline {
    agent any
    stages {
        stage("Package") {
            steps {
                sh "./gradlew build"
            }
        }
        stage("Docker build") {
            steps {
                // Correctly tag the image
                sh "docker build -t localhost:5000/calculatrice ."
            }
        }
        stage("Docker push") {
            steps {
                sh "docker push localhost:5000/calculatrice"
            }
        }
        stage("Deploy to staging ou Déployer en préproduction") {
            steps {
                // Stop and remove the container if it's already running
                sh "docker rm -f calculatrice || true"
                
                // Run the new container
                sh "docker run -d --rm -p 8769:8080 --name calculatrice localhost:5000/calculatrice"
            }
        }
    }
}


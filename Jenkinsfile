pipeline {
    agent any
    environment {
        // Utilisation d'une variable d'environnement pour récupérer la version Git actuelle
        VERSION = sh(script: "git rev-parse --short HEAD", returnStdout: true).trim()
        IMAGE_NAME = "localhost:5000/calculatrice"
    }
    stages {
        stage("Package") {
            steps {
                // Construction du projet avec Gradle
                sh "./gradlew build"
            }
        }
        stage("Docker build") {
            steps {
                // Taguer l'image avec le hash Git pour le versionnement
                sh "docker build -t ${IMAGE_NAME}:${VERSION} ."
            }
        }
        stage("Docker push") {
            steps {
                // Pousser l'image versionnée dans le registre local
                sh "docker push ${IMAGE_NAME}:${VERSION}"
            }
        }
        stage("Deploy to staging ou Déployer en préproduction") {
            steps {
                // Arrêter et supprimer le conteneur existant si nécessaire
                sh "docker rm -f calculatrice || true"
                
                // Exécuter le conteneur avec la version de l'image
                sh "docker run -d --rm -p 8769:8080 --name calculatrice ${IMAGE_NAME}:${VERSION}"
            }
        }
        stage("Acceptance test") {
          steps {
         sleep 60
        sh "chmod +x acceptance_test.sh && ./acceptance_test.
sh"
}
}
    }
}


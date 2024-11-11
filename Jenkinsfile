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
        sh "docker build -t calculatrice ."
        
    }
}
stage("Docker push") {
    steps {
        sh "docker push localhost:5000/calculatrice"
    }
}
       
      }
}

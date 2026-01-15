pipeline {
    agent { label "ubuntu" }
    
    stages {
        
        stage("Code clone") {
           steps {
           echo "This is cloning steps"
           sh "whoami"
           git branch: 'main', url: 'https://github.com/dakorat23/django-notes-app.git'
           echo "Code cloned successfully"
         } 
        }
        
        stage ("build") {
            steps {
            echo "This is build steps"
            sh "whoami"
            sh "docker build -t notes-app:latest ."
            }
        }
        
        stage ("Push to Dockerhub") {
            steps {
            withCredentials([
            usernamePassword(
                credentialsId: 'docker-hub-creds',
                usernameVariable: 'DOCKER_USER',
                passwordVariable: 'DOCKER_PASS')]){
                sh """
                echo \$DOCKER_PASS | docker login -u \$DOCKER_USER --password-stdin
                docker image tag notes-app:latest \$DOCKER_USER/django-notes-app:latest
                docker push \$DOCKER_USER/django-notes-app:latest
                echo "This is test steps"
                """
            }
        }
        }
        
        stage ("deploy") {
            steps { 
            echo "This is deploy steps"
            sh "docker run -t -d -p 8000:8000 notes-app:latest "
            }
        }
     }
}

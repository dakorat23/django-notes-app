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
        
        stage ("test") {
            steps {
            echo "This is test steps"
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

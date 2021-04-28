pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
               
               bat 'mvn -Dmaven.test.failure.ignore=true clean package'
               }
               }
               
               
       stage('Building image') {
            steps{
                
         bat 'docker build -f src/main/docker/Dockerfile.jvm -t quarkus/hello-world-jvm .'
            }
            }
            stage('Deploying into k8s'){
            steps{
                   
                bat 'kubectl apply -f deployment.yaml'
                        }
            }
            
            
        }
        }
        

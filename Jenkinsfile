pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
               
               sh 'java -jar target/getting-started-1.0-SNAPSHOT-runner.jar'
               }
               }
               
               
       stage('Building image') {
            steps{
                
         sh 'docker build -f src/main/docker/Dockerfile.jvm -t quarkus/hello-world-jvm .'
            }
            }
            stage('Deploying into k8s'){
            steps{
                   
                sh 'kubectl apply -f deployment.yaml'
                        }
            }
            
            
        }
        }
        

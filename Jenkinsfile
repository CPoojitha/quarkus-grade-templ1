pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
               
               sh './mvnw -Dmaven.test.failure.ignore=true clean package'
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
        


pipeline {

agent {
        kubernetes {
      yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: test-odu
    label : jenkins
spec:
  securityContext:
    runAsUser: 10000
    runAsGroup: 10000
  containers:
  - name: jnlp
    image: 'jenkins/jnlp-slave:4.3-4'
    args: ['\$(JENKINS_SECRET)', '\$(JENKINS_NAME)']
  - name: yair
    image: us.icr.io/dc-tools/security/yair:1
    command:
    - cat
    tty: true
    imagePullPolicy: Always
  - name: kaniko
    image: gcr.io/kaniko-project/executor:debug-1534f90c9330d40486136b2997e7972a79a69baf
    imagePullPolicy: Always
    command:
    - cat
    tty: true
    volumeMounts:
      - name: regsecret
        mountPath: /kaniko/.docker
    securityContext: # https://github.com/GoogleContainerTools/kaniko/issues/681
      runAsUser: 0
      runAsGroup: 0
  - name: openshift-cli
    image: openshift/origin-cli:v3.11.0
    command:
    - cat
    tty: true
    securityContext: # https://github.com/GoogleContainerTools/kaniko/issues/681
      runAsUser: 0
      runAsGroup: 0
  volumes:
  - name: regsecret
    projected:
      sources:
      - secret:
          name: regsecret
          items:
            - key: .dockerconfigjson
              path: config.json
  imagePullSecrets:
  - name: oduregsecret
  - name: regsecret
"""
        }
    }
  environment {
    
     /* -----------DevOps Commander  created env variables------------ */
	
	DOCKER_URL= "us.icr.io/dc-tools"
DOCKER_CREDENTIAL_ID= "dc-docker-6110"
OPENSHIFT_URL= "https://c100-e.us-south.containers.cloud.ibm.com:32634/"
OPENSHIFT_CREDENTIAL_ID= "dc-openshift-6110"
SONARQUBE_URL= "https://sonarqube-3-6.container-crush-02-4044f3a4e314f4bcb433696c70d13be9-0000.eu-de.containers.appdomain.cloud/"
SONARQUBE_CREDENTIAL_ID= "dc-sonarqube-6110"
CLAIR_URL= "https://clair-3-3.container-crush-02-4044f3a4e314f4bcb433696c70d13be9-0000.eu-de.containers.appdomain.cloud/"
CLAIR_CREDENTIAL_ID= "dc-clair-6110"
NAMESPACE= "tools-dev"
INGRESS= "isdc20-0ce42e8480356580312b8efcc5f21aad-0001.us-south.containers.appdomain.cloud"
	
	/* -----------DevOps Commander  created env variables------------ */

          VERSION="1-SNAPSHOT"

        /* Parameters for Docker image that will be built and deployed */
        /* REGISTRY_USERNAME provided via a Jenkins secret
         * REGISTRY_PASSWORD provided via a Jenkins secret
         */
        REGISTRY_NAME="us.icr.io/dc-tools"
	//REGISTRY_NAME="odureg.azurecr.io"
        REGISTRY_SECRET="odu-registry"
        DOCKER_IMAGE="lnk"
        DOCKER_TAG="$BUILD_NUMBER"
	K8S_DEPLOYMENT="nodejs-test"
       
  }
 
  stages {
    
      stage('Build'){
       
            steps{
             script{
                  sh ' ./mvn -Dmaven.test.failure.ignore=true clean package'
                }
            }
        }

       
        
	
	
        


    }
}


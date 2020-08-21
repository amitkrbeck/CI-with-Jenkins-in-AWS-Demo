pipeline {
        agent any
        environment {
            registry = "amitkrbeck/sp6k8s"
            registryCredential = 'dockerhub'
            dockerImage = ''
		PROJECT_ID = 'ace-apex-278213'
 		CLUSTER_NAME = 'amit-k8s-cluster'
 		LOCATION = 'us-central1-c'
 		CREDENTIALS_ID = 'amit-k8-cluster'
        }
		
	    stages {	
		   stage('Scm Checkout') {            
			steps {
	                  checkout scm
			}	
	           }     
            }
	           stage('Deploy to GKE') {
 			steps{
 				echo "Deployment started"
				sh 'ls -ltr'
				sh 'pwd'
				sh "sed -i 's/tagversion/${env.BUILD_ID}/g' deployment.yaml"
				step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID,
				      clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'deployment.yaml',
				      credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
				echo "Deployment Completed"
 	            }
	          }
	    }

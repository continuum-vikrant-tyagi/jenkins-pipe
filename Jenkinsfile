pipeline {
  agent none
  stages {
    stage('Run go') {
      agent {
        kubernetes {
        //cloud 'kubernetes'
        label 'tyagipod'
        yamlFile 'KubernetesPod.yaml'
        }
      }
      tools {
        go 'go'
      }
      steps {
        container('nodego') {
          sh 'echo $GOROOT'
          sh "go env"
          
        }
      }
    }
	
	 stage('build-docker') {
	  agent {
      kubernetes {
      //cloud 'kubernetes'
      label 'kaniko'
      yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: kaniko
    image: gcr.io/kaniko-project/executor:latest
    args: ["--dockerfile=Dockerfile",
           "--context=$WORKSPACE"]
"""
     }
   }
     steps {
      echo 'Hello kaniko'
     }
    
	  }
  }
 }
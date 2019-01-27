pipeline {
  agent {
    kubernetes {
      //cloud 'kubernetes'
      label 'tyagipod'
      yamlFile 'KubernetesPod.yaml'
    }
  }
  stages {
    stage('Run go') {
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
    image: gcr.io/kaniko-project/executor:debug
    command: ['cat']
    tty: true
"""
     }
    
	  }
   }
  }
 }
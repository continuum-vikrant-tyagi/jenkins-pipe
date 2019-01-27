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
      
      //tools {
        //go 'go'
      //}
      steps {
        container('nodego') {
          //sh 'echo $GOROOT'
          //sh "go env"
          dir(WORKSPACE) {
            sh 'cp dockerfile /var/sharedvolume'
            sh 'cp hello.html /var/sharedvolume'
          }
          
        }
      }
    }
	
	 stage('build-docker') {
    agent {
    kubernetes {
    yaml """
apiVersion: v1
kind: Pod
metadata:
  name: kaniko
spec:
  containers:
    - name: kaniko
      image: gcr.io/kaniko-project/executor:debug
      args: ["--dockerfile=dockerfile",
             "--context=/kaniko/sharedvolume"]
      volumeMounts:
        - name: sharedvolume
          mountPath: '/kaniko/sharedvolume' 
      resources:
        requests:
          cpu: "50m"
          memory: "124Mi"
        limits:
          cpu: "2000m"
          memory: "2048Mi"
"""
    }
   }  
   }
 }
}
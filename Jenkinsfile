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
          dir(WORKSPACE) {
            sh "cp dockerfile /opt/app/shared"
          }
          
        }
      }
    }
	
	 stage('build-docker') {
	  //agent {
      //kubernetes {
      //cloud 'kubernetes'
      //label 'kaniko'
      //yaml """
//apiVersion: v1
//kind: Pod
//spec:
  //containers:
  //- name: kaniko
    //image: gcr.io/kaniko-project/executor:debug
    //args: ["--dockerfile=dockerfile",
           //"--context=/opt/app/shared"]
    //volumeMounts:
      //- name: sharedvolume
        //mountPath: '/opt/app/shared'
//"""
     //}
   //}
     steps {
      container('kaniko')
      sh 'ls /opt/app/shared/dockerfile ; echo $?'
     }
    
	  }
  }
 }
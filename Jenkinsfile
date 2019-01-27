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
       steps {
         container('kaniko') {
            echo 'Hello kaniko'
            //sh 'ls -ltr /var/sharedvolume'
    
            sh 'sleep 60'
         }
        }  
      }
 }
}
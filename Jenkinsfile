pipeline {
  agent {
        kubernetes {
        //cloud 'kubernetes'
        label 'tyagipod'
        yamlFile 'KubernetesPod.yaml'
        }
      }
  environment {
        PATH = "/busybox:/kaniko:$PATH"
      }
  stages {
    stage('Run go') {
      
      //tools {
        //go 'go'
      //}
      steps {
        container('nodego') {
          sh 'echo $GOROOT'
          sh "go env"
          dir(WORKSPACE) {
            sh 'cp dockerfile /var/sharedvolume'
            sh 'cp hello.html /var/sharedvolume'
          }
          
        }
      }
    }
	
	  stage('build-docker') {
       steps {
         container(name: 'kaniko', shell: '/busybox/sh') {
            sh '''#!/busybox/sh
            /kaniko/executor -f `pwd`/dockerfile -c `pwd` --insecure --skip-tls-verify --cache=false --no-push
            '''
         }
        }  
      }
 }
}
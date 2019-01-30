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
	 stage('Run') {
    parallel {
     stage('hello') {
        steps {
          container('nodego') {
            sh 'echo hello nodego'
          }
        }
    }
    
    stage('build-dockerImage') {
        steps {
         container(name: 'kaniko', shell: '/busybox/sh') {
            sh '''#!/busybox/sh
            /kaniko/executor -f $WORKSPACE/dockerfile -c `pwd` --insecure --skip-tls-verify --cache=true --destination=https://index.docker.io/v1/tyagivasu/ngnix:latest
            '''
            sleep(60)
         }
        }  
      }
    }
   }    
 }
}
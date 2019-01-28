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
	
	  stage('build-docker') {
       steps {
         container(name: 'kaniko', shell: '/busybox/sh') {
           //sh '''#!/busybox/sh
            ///kaniko/executor -f `pwd`/dockerfile -c `pwd` --insecure --skip-tls-verify --cache=false --no-push
            //'''
            sh '''#!/busybox/sh
            /kaniko/executor -f $WORKSPACE/dockerfile -c `pwd` --insecure --skip-tls-verify --cache=false --no-push
            '''
         }
        }  
      }
 }
}
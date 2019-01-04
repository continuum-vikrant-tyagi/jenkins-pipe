pipeline {
  agent {
    kubernetes {
      //cloud 'kubernetes'
      label 'tyagi-pod'
      yaml 'KubernetesPod.yaml'
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
          
          
        }
      }
    }
}
}
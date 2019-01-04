pipeline {
  agent {
    kubernetes {
      //cloud 'kubernetes'
      label 'tyagipod'
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

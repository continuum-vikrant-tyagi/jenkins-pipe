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
          
          
        }
      }
    }
}
}

pipeline {
  agent {
    kubernetes {
      //cloud 'kubernetes'
      label 'tyagipod'
      yamlFile 'KubernetesPod.yaml'
    }
  }
  parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')

        file(name: "FILE", description: "Choose a file to upload")
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
	
	stage('Parameter') {
	  steps {
	    container('nodego') { 
		  
		  echo "Hello ${params.PERSON}"

          echo "Biography: ${params.BIOGRAPHY}"

          echo "Toggle: ${params.TOGGLE}"

          echo "Choice: ${params.CHOICE}"

          echo "Password: ${params.PASSWORD}"
		}
	}
}
}
}

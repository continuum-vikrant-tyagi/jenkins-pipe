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
	
	stage('Upload') {
	  steps {
	    container('nodego') { 
		//sh "printenv"
           	sh 'mkdir -p $WORKSPACE/continuum/agentService'
           	sh 'mkdir -p $WORKSPACE/continuum/api'
           	sh 'mkdir -p $WORKSPACE/scripts'
           	sh 'mkdir -p $WORKSPACE/config'
          	sh 'apt-get install zip -y'
           	dir(WORKSPACE){
           	sh 'zip -r continuum.zip continuum'
           	sh 'zip -j platformagentservicedeploy.zip continuum.zip'
           	}
           	rtUpload (
                    serverId: "Artifactory-1",
                    spec: """{
                            "files": [
                                    {
                                        "pattern": "$WORKSPACE/platformagentservicedeploy.zip",
                                        "target": "test-jenkin-pipeline/$JOB_BASE_NAME/$BUILD_NUMBER/"
                                    }
                                ]
                            }"""
                )
           	sh 'sleep 60'    
	   }
	}
}
}
}

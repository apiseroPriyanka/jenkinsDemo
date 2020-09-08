pipeline {
  agent any
  stages {
    stage('Build Application') { 
      steps {
        bat 'mvn clean install'
      }
    }
 	stage('Test') { 
      steps {
        echo 'Test Appplication...' 
        bat 'mvn test'
      }
    }
 	
   
	stage('Deploy CloudHub') { 
      environment {
        ANYPOINT_CREDENTIALS = credentials('anypointPlatform')
      }
      steps {
        sh 'mvn deploy -P cloudhub -Dmule.version=4.3.0
		-Danypoint.username=${ANYPOINT_CREDENTIALS_USR} 
		-Danypoint.password=${ANYPOINT_CREDENTIALS_PSW}
		-DworkerType=Micro 
		-Dworkers=1 
		-Dregion=us-west-2' 
      }
    }
  }
}

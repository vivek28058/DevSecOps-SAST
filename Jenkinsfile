pipeline {
  agent any
  tools { 
        maven 'maven_3_9_9'  
    }
   stages{
    stage('Run SCA Analysis using Snyk') {
            steps {		
			withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
			    bat 'mvn snyk:test -X'
				}
			}
    }	


  }
}

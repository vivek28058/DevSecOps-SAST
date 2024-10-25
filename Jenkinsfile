pipeline {
  agent any
  tools { 
        maven 'maven_3_5_2'  
    }
   stages{
    stage('Run SCA Analysis using Snyk') {
            steps {		
			withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
			    bat 'mvn snyk:test -fn'
				}
			}
    }	


  }
}

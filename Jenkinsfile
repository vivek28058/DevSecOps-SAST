pipeline {
  agent any
  tools { 
        maven 'maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=franksast -Dsonar.organization=franksast -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=ce3caf6f60b599b72a6ced8a5fc17e060b1d87ee'
		//sh 'mvn clean compile sonar:sonar -Dsonar.projectKey=franksast -Dsonar.organization=franksast -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=ce3caf6f60b599b72a6ced8a5fc17e060b1d87ee'
			}
        } 
  }
}

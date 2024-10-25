pipeline {
    agent any
    tools { 
        maven 'maven_3_9_9'  
    }
    stages {
        stage('Run SCA Analysis using Snyk') {
            steps {		
                withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
                    // Run Snyk SCA analysis
                    bat 'mvn snyk:test -fn'
                }
            }
        }
        stage('Upload Results to Snyk Dashboard') {
            steps {
                withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
                    // Upload results to Snyk dashboard
                    bat 'mvn snyk:monitor'
                }
            }
        }
    }
}

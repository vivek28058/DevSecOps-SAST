pipeline {
    agent any

    environment {
        SNYK_TOKEN = credentials('SNYK_TOKEN') // Ensure you have this set in Jenkins credentials
    }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('Run SCA Analysis using Snyk') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
			        bat 'mvn snyk:test -fn'
                }
            }
        }
        stage('Report Issues to Snyk') {
            steps {
                script {
                    def snykIssues = []
                    // Parse the snykOutput for issues
                    def issueRegex = /[^\n]+?(Critical|High|Medium|Low) Severity\[([^\]]+)\]/ // Adjust regex based on output format
                    snykOutput.eachLine { line ->
                        def matcher = (line =~ issueRegex)
                        if (matcher) {
                            snykIssues.add(line)
                        }
                    }
                    
                    // Log issues for debugging
                    if (snykIssues.size() > 0) {
                        echo "Found the following issues:"
                        snykIssues.each { echo it }
                        
                        // Push results to Snyk Dashboard
                        def result = bat(script: "snyk monitor --all-sub-projects", returnStdout: true)
                        echo "Snyk monitor result: ${result}"
                    } else {
                        echo "No issues found."
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // Add any necessary cleanup steps
        }
    }
}
}

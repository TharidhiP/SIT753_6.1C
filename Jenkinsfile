pipeline{
    agent any
    environment {
        DIRECTORY_PATH='Test Path'
        TESTING_ENVIRONMENT='Test Environment'
        PRODUCTION_ENVIRONMENT='Tharidhi'
    }
    stages{
        stage('Build'){
            steps{
                echo "fetch the source code from the ${env.DIRECTORY_PATH} specified by the environment varaible"
                echo "compile the code and generate any necessary artifacts"
                script{
                    def mavenVersion = bat(script: 'mvn --version', returnStdout: true).trim()
                    echo "Maven Version: ${mavenVersion}"
                }
            }
        }
        
        stage('Test'){
            steps{
                echo "unit tests"
                sh "junit --version"
                echo "integration tests"
                sh "jmeter --version"
            }
            post {
                success {
                    // Send email notification on success
                     emailext (
                        subject: "Build Status Email",
                        body: "Test stage was successful",
                        to: "tharidhip172002@gmail.com"
                    )
                }
                failure {
                    // Send email notification on failure
                     emailext (
                        subject: "Build Status Email",
                        body: "Test stage was unsuccessful",
                        to: "tharidhip172002@gmail.com"
                    )
                }
            }
        }
        
        stage('Code Analysis'){
            steps{
                echo "do a security scan of the code"
                //sh "snyk --version"
            }
        }

        stage('Security Scan'){
            steps{
                echo "check the quality of the code"
                //sh "sonarqube --version"
            }
             post {
                success {
                    // Send email notification on success
                     emailext (
                        subject: "Build Status Email",
                        body: "Security scan stage was successful",
                        to: "tharidhip172002@gmail.com"
                    )
                }
                failure {
                    // Send email notification on failure
                    emailext (
                        subject: "Build Status Email",
                        body: "Security scan was unsuccessful",
                        to: "tharidhip172002@gmail.com"
                    )
                }
            }
        }
        
        stage('Deploy to Staging Environment'){
            steps{
                echo "deploy the application to ${env.TESTING_ENVIRONMENT} specified by the environment variable"
            }
        }
         stage('Test in Staging Environment'){
            steps{
                echo "integration tests"
                //sh "jmeter --version"
            }
        }
         stage('Deploy to Production'){
            steps{
                echo "fetch the source code from the ${env.DIRECTORY_PATH} specified by the environment variable"
                echo "${env.PRODUCTION_ENVIRONMENT}, production environment deployment done"
            }
        }
        
    }
}

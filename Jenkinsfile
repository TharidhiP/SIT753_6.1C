pipeline {
    agent any
    environment {
        DIRECTORY_PATH='Test Path'
        TESTING_ENVIRONMENT='Test Environment'
        PRODUCTION_ENVIRONMENT='Tharidhi'
    }
    stages {
        stage('Build') {
            steps {
                echo "fetch the source code from the ${env.DIRECTORY_PATH} specified by the environment variable"
                echo "compile the code and generate any necessary artifacts"
                script {
                    def mavenVersion = bat(script: 'mvn --version', returnStdout: true).trim()
                    echo "Maven Version: ${mavenVersion}"
                }
            }
        }
        
        stage('Test') {
            steps {
                echo "unit tests"
                script {
                    def junitVersion = bat(script: 'java -cp junit-platform-console-standalone.jar --version', returnStdout: true).trim()
                    echo "JUnit Version: ${junitVersion}"
                }
                echo "integration tests"
                script {
                    def junitVersion = bat(script: 'java -cp junit-platform-console-standalone.jar --version', returnStdout: true).trim()
                    echo "JUnit Version: ${junitVersion}"
                }
            }
            post {
                always {
                    script {
                        // Define the recipient's email address
                        def recipient = "tharidhip172002@gmail.com"
                        
                        // Define the subject and body of the email
                        def subject
                        def body
                        
                        // Check the build result and set subject and body accordingly
                        if (currentBuild.result == 'SUCCESS') {
                            subject = "Test Stage Successful"
                            body = "The test stage was successful. Click the following link to view the console output: ${env.BUILD_URL}/console"
                        } else {
                            subject = "Test Stage Failed"
                            body = "The test stage failed. Click the following link to view the console output: ${env.BUILD_URL}/console"
                        }
                        
                        // Send the email
                        mail (
                            to: recipient,
                            subject: subject,
                            body: body
                        )
                    }
                }
            }
        }
        
        stage('Code Analysis') {
            steps {
                echo "do a security scan of the code"
                script {
                    def javaVersion = bat(script: 'java -version', returnStdout: true).trim()
                    echo "Java Version: ${javaVersion}"
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo "check the quality of the code"
                script {
                    def javaVersion = bat(script: 'java -version', returnStdout: true).trim()
                    echo "Java Version: ${javaVersion}"
                }
            }
            post {
                always {
                    script {
                        // Define the recipient's email address
                        def recipient = "tharidhip172002@gmail.com"
                        
                        // Define the subject and body of the email
                        def subject
                        def body
                        
                        // Check the build result and set subject and body accordingly
                        if (currentBuild.result == 'SUCCESS') {
                            subject = "Security Scan Successful"
                            body = "The security scan stage was successful. Click the following link to view the console output: ${env.BUILD_URL}/console"
                        } else {
                            subject = "Security Scan Failed"
                            body = "The security scan stage failed. Click the following link to view the console output: ${env.BUILD_URL}/console"
                        }
                        
                        // Send the email
                        mail (
                            to: recipient,
                            subject: subject,
                            body: body
                        )
                    }
                }
            }
        }
        
        stage('Deploy to Staging Environment') {
            steps {
                echo "deploy the application to ${env.TESTING_ENVIRONMENT} specified by the environment variable"
            }
        }
        
        stage('Test in Staging Environment') {
            steps {
                echo "integration tests"
                script {
                    def junitVersion = bat(script: 'java -cp junit-platform-console-standalone.jar --version', returnStdout: true).trim()
                    echo "JUnit Version: ${junitVersion}"
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo "fetch the source code from the ${env.DIRECTORY_PATH} specified by the environment variable"
                echo "${env.PRODUCTION_ENVIRONMENT}, production environment deployment done"
            }
        }
    }
}






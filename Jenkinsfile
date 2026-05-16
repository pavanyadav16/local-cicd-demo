pipeline {
    agent any

    tools {
        // This tells Jenkins to use the Maven environment configured in your system
        maven 'Default' 
        jdk 'Default'
    }

    stages {
        stage('Checkout') {
            steps {
                // Pulls the latest code from GitHub
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Uses Windows batch command to run Maven package
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                // Runs automated tests
                bat 'mvn test'
            }
        }

        stage('Deploy Locally') {
            steps {
                // Kills any existing Java processes running on port 8080 to free it up
                // Then starts the new built jar in the background
                script {
                    bat '''
                    FOR /F "tokens=5" %%a IN ('netstat -aon ^| find ":8080" ^| find "LISTENING"') DO taskkill /F /PID %%a || echo Port 8080 is free.
                    start "JavaApp" java -jar target/cicd-demo-1.0.0.jar
                    '''
                }
            }
        }
    }
}
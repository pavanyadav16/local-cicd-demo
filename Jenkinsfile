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
                script {
                    // This is the magic line! It tells Jenkins NOT to kill our background app
                    env.JENKINS_NODE_COOKIE = 'dontKillMe'
                    
                    bat '''
                    @echo off
                    echo Cleaning up port 8080...
                    FOR /F "tokens=5" %%a IN ('netstat -aon ^| find ":8080" ^| find "LISTENING"') DO taskkill /F /PID %%a || echo Port 8080 is free.
                    
                    echo Starting Application...
                    :: We use cmd /c to run it and redirect output to app.log for troubleshooting
                    start "JavaApp" cmd /c "java -jar target/cicd-demo-1.0.0.jar > app.log 2>&1"
                    '''
                }
            }
        }
    }
}
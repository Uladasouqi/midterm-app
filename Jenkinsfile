pipeline {
    agent any

    tools {
        maven 'Maven 3'
        jdk 'JDK17'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning the GitHub repository...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building the Spring Boot fat JAR...'
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Archive') {
            steps {
                echo 'Archiving the JAR artifact...'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Build completed successfully!'
        }
        failure {
            echo '❌ Build failed. Check logs for errors.'
        }
    }
}

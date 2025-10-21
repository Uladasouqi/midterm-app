pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Pulling source code from GitHub...'
                checkout scm
            }
        }

        stage('Build Fat JAR') {
            steps {
                echo 'Building project with Maven...'
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Archive Artifact') {
            steps {
                echo 'Archiving the generated JAR file...'
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Build succeeded! Fat JAR created and archived.'
        }
        failure {
            echo '❌ Build failed. Check the console output for errors.'
        }
    }
}

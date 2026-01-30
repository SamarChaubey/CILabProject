pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'JDK17'
    }

    stages {

        stage('Prepare') {
            steps {
                echo "Branch: ${env.BRANCH_NAME}"
            }
        }

        stage('Build') {
            when {
                branch 'main'
            }
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Security Scan') {
            when {
                expression { env.BRANCH_NAME.startsWith('release') }
            }
            steps {
                echo 'Security scan placeholder'
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
        }
    }
}

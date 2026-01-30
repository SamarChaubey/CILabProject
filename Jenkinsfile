pipeline {
    agent any

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
                echo 'Building with Maven'
                bat 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests'
                bat 'mvn test'
            }
        }

        stage('Security Scan') {
            when {
                expression { env.BRANCH_NAME.startsWith('release') }
            }
            steps {
                echo 'Running security scan (placeholder)'
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
        }
    }
}

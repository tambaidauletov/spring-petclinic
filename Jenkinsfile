pipeline {
    agent any

    triggers {
        cron('H/3 * * * 1') // Runs every 3 minutes on Mondays
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo "Building the Spring Petclinic project..."
                    sh './mvnw clean package'
                }
            }
        }

        stage('Code Coverage') {
            steps {
                script {
                    echo "Running tests and generating JaCoCo code coverage report..."
                    sh './mvnw test jacoco:report'
                }
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
            jacoco execPattern: '**/target/jacoco.exec'
        }
    }
}

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
                    bat './mvnw.cmd clean package'
                }
            }
        }

        stage('Code Coverage') {
            steps {
                script {
                    echo "Running tests and generating JaCoCo code coverage report..."
                    bat './mvnw.cmd test jacoco:report'
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

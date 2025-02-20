pipeline {
    agent any
    triggers {
        cron('H/10 * * * 1')
    }
    stages {
        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
                }
            }
        }
        stage('Code Coverage') {
            steps {
                sh './mvnw test'
                jacoco execPattern: '**/target/*.exec'
            }
            post {
                always {
                    jacoco execPattern: '**/target/*.exec', classPattern: '**/classes', sourcePattern: '**/src/main/java'
                }
            }
        }
    }
}

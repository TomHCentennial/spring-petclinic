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
            }
            post {
                always {
                    jacoco execPattern: '**/target/*.exec', classPattern: '**/target/classes', sourcePattern: '**/src/main/java'
                }
            }
        }
    }
    post {
        always {
            junit '**/target/surefire-reports/*.xml'
        }
    }
}

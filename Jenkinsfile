// Declarative //
pipeline {
    agent {
        docker {
            image 'maven:3.6.1-alpine'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                echo 'Starting Build Project'
                sh 'mvn -B -DskipTests clean package'
                echo 'Finished Build Project'
            }
        }
        stage('Test') {
            steps {
                echo 'Starting Test Project'
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Manual Approval') {
            steps {
                input message: 'Lanjutkan ke tahap Deploy?'
            }
        }
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                sleep 60
            }
        }
    }
}
// Script //
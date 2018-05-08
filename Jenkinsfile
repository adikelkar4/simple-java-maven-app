pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage('Building') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('Testing') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Delivering') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
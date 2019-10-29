pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
		# sh 'mvn clean install -DproxySet=true -DproxyHost=135.245.48.34 -DproxyPort=8000'
                sh 'mvn -B -DproxySet=true -DproxyHost=135.245.48.34 -DproxyPort=8000 -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}

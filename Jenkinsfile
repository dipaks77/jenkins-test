pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building'
                sh './gradlew build'
                archiveArtifacts artifacts: 'dist/reactJest.zip'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying asad'
            }
        }
    }
}

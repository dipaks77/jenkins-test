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
        stage('Deploying to staging') {
            when {
                branch 'master'
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'staging_webserver', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
                    sshPublisher(
                        failOnError: true,
                        continueOnError: false,
                        publishers: [
                            sshPublisherDesc(
                                configName: 'staging',
                                sshCredentials: [
                                    username: '$USERNAME',
                                    encryptedPassphrase: '$USERPASS'
                                ],
                                transfers: [
                                    sshTransfer(
                                        sourceFiles: 'dist/reactJest.zip',
                                        removePrefix: 'dist/',
                                        remoteDirectory: '/tmp',
                                        execCommand: 'unzip /tmp/reactJest.zip'
                                    )
                                ]
                            )
                        ]
                    )
                }
            }
        }
    }
}

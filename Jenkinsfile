pipeline{
agent any

    
    
    stages {
        stage('TEST') {
            steps {
                script {
                    echo 'Running tests...'
                    sh './gradlew test'

                }
            }

}




                        stage('BUILD') {
                            steps {
                                script {
                                    echo 'Building the project...'

                                    sh './gradlew build'
                                }
                            }
                        }

                                stage('DEPLOY') {
                                    steps {
                                        script {
                                            echo 'Deploying the application...'
                                            sh './gradlew publish'
                                        }
                                    }
                                }


                                stage('NOTIFY') {
                                    steps {
                                        script {
                                            echo 'Sending email notification...'

                                            sh './gradlew sendMail'
                                            sh './gradlew notifySlack'
                                            echo 'Sending email...'
                                                        mail to: 'chatgpties210@gmail.com',
                                                             subject: "Jenkins Build: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                                                             body: """\
                                                             The build has completed.

                                                             Build Details:
                                                             - Job: ${env.JOB_NAME}
                                                             - Build Number: ${env.BUILD_NUMBER}
                                                             - Status: ${currentBuild.currentResult}
                                                             - URL: ${env.BUILD_URL}
                                                             """



                                        }
                                    }
                                }
                            }
}

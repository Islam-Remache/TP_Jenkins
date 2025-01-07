pipeline{
agent any




    
    stages {
        stage('TEST') {
            steps {
                script {
                    echo 'Running tests.....'
                    sh './gradlew test'

                }


                }
                                post {
                                    always {
                                        cucumber '**/reports/*.json'

                                    }
            }

}

        stage('CODEANALYSIS') {


            steps {
                script {
                    echo 'Running SonarQube analysis...'
                    withSonarQubeEnv('sonar') {
                        sh './gradlew sonarqube'
                    }
                }
            }
        }

      /*  stage('CODEQUALITY') {
                             steps {
                                script {
                                    echo 'Checking SonarQube Quality Gate...'
                                   def qualityGate = waitForQualityGate()
                                     if (qualityGate.status != 'OK') {
                                         error "SonarQube Quality Gate failed: ${qualityGate.status}"
                                    }
                                }
                            }
                        }*/


                        stage('BUILD') {
                            steps {
                                script {
                                    echo 'Building the project...'

                                    sh './gradlew build'
                                    archiveArtifacts artifacts: '**/build/libs/*.jar, **/build/docs/**/*', allowEmptyArchive: true
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


                                stage('NOTIFYEMAIL') {
                                    steps {
                                        script {
                                            echo 'Sending email notification...'

                                            sh './gradlew sendMail'

                                            /*echo 'Sending email...'
                                                        mail to: 'chatgpties210@gmail.com',
                                                             subject: "Jenkins Build: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                                                             body: """\
                                                             The build has completed.

                                                             Build Details:
                                                             - Job: ${env.JOB_NAME}
                                                             - Build Number: ${env.BUILD_NUMBER}
                                                             - Status: ${currentBuild.currentResult}
                                                             - URL: ${env.BUILD_URL}
                                                             """*/



                                        }
                                    }
                                }


                        stage('NOTIFYSLACK') {
                                    steps {
                                        // script {
                                        //     echo 'Sending message notification with slack...'
                                        //     // Call Gradle sendMail task
                                        //     sh 'gradle notifySlack'
                                        // }
                                        slackSend channel: '#ogl-project',
                                            color: 'good',
                                            message: ':rocket: *Deploiement termine avec succes!* :tada:'
                                    }
                                }

                            }
}

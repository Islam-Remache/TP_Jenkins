pipeline{
agent any




    
    stages {

        stage('test') {
            steps {
                script {
                    echo 'Tests en cours.....'
                    sh './gradlew test'

                }


                }
                post {
                    always {
                        cucumber '**/reports/*.json'

                    }
            }

}



        stage('AnalyseCode') {


            steps {
                script {
                    echo 'Analyse Sonarqube en cours...'
                    withSonarQubeEnv('sonar') {
                        sh './gradlew sonarqube'
                    }
                }
            }
        }



      stage('QualityGate') {
                             steps {
                                script {
                                    echo 'SonarQube Quality Gate Test en cours...'
                                   def qualityGate = waitForQualityGate()
                                     if (qualityGate.status != 'OK') {
                                         error "echec dans SonarQube Quality Gate : ${qualityGate.status}"
                                    }
                                }
                            }
                        }


                        stage('Build') {
                            steps {
                                script {
                                    echo 'Build du projet...'

                                    sh './gradlew build'
                                }
                            }
                        }

                        stage('ArchiverArtifacts') {
                            steps {

                                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
                                archiveArtifacts artifacts: 'build/reports/tests/**/*', fingerprint: true
                                archiveArtifacts artifacts: 'build/reports/cucumber/**/*', fingerprint: true
                            }
                        }



                                stage('Deploy') {
                                    steps {
                                        script {
                                            echo 'Deploiement de le application...'
                                            sh './gradlew publish'
                                        }
                                    }
                                }


                                stage('NotifEmail') {
                                    steps {
                                        script {
                                            echo 'Nnotification Email envoye...'

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


                        stage('NotifSlack') {
                                    steps {

                                        slackSend channel: '#ogl-project',
                                            color: 'good',
                                            message: ':rocket: *Deploiement termine avec succes!* :tada:'
                                    }
                                }

                            }
}

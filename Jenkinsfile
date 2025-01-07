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
                                        }
                                    }
                                }
                            }
}

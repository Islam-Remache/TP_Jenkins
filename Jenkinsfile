pipeline{
agent any

    

    environment {
    GITHUB_CREDENTIALS = 'github-credentials'
}
    
    
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
}

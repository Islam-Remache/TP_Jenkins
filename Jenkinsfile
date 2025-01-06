pipeline{
agent any

    

    environment {
    GITHUB_CREDENTIALS = 'github-credentials'
                MAVEN_REPO_USERNAME = credentials('github-credentials')  // Replace with your actual Jenkins credential ID
        MAVEN_REPO_PASSWORD = credentials('github-credentials')
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

pipeline {
    agent any
	
    stages {
        stage('Clone Repository') {
            steps {
               git branch: 'develop', url: 'https://github.com/madamanchisathish/sample-java-application.git'
            }
        }
    }
}


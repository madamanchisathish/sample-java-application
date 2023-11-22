pipeline {
    agent any
	
    stages {
        stage('GitHub Clone Repository') {
            steps {
               git branch: 'future', url: 'https://github.com/madamanchisathish/sample-java-application.git'
			   echo "GitHub Repository Clone Successfully"
            }
        }
		
		stage('Maven Build and Test') {
            steps {
                script {
                    // Run Maven build and test
                    sh 'mvn clean package'
					echo "Maven Build Successfully"
                }
            }
        }
    }
}


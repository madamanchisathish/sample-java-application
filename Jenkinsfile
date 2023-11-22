pipeline {
    agent any
	
    stages {
        stage('GitHub Clone Repository') {
            steps {
               git branch: 'future', url: 'https://github.com/madamanchisathish/sample-java-application.git'
			   echo "GitHub Repository Clone Successfully"
            }
        }
		
		stage('Maven Build and Generate Artifact') {
            steps {
                script {
                    // Run Maven build and test
                    sh 'mvn clean package'
					echo "Maven Build Successfully"
                }
            }
        }
		
		stage('SonarQube - Testing') {
          steps {
            sh "mvn sonar:sonar \
            -Dsonar.projectKey=sample-app \
            -Dsonar.host.url=http://18.222.25.49:9000 \
            -Dsonar.login=dd859a7944049d3261946025f8455464a9db7ece"
          }
        }
    }
}


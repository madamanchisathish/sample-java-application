pipeline {
    agent any
	
	environment {
        // Define environment variables
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials') // ID of your Docker Hub credentials in Jenkins
        IMAGE_TAG = "madamanchisathish/java-sample:latest" // Replace with your Docker Hub username and image name
    }
	
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
			echo "SonarQube Testing Successfully"
          }
        }
		
		stage('Build Docker Image') {
            steps {
                script {
                    // Building Docker Image
                    sh "docker build -t ${IMAGE_TAG} ."
					echo "Create Docker Image Successfully"
                }
            }
        }
    }
}


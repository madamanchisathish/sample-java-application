pipeline {
    agent any
	
	environment {
        // Define environment variables
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials') // ID of your Docker Hub credentials in Jenkins
        IMAGE_TAG = "madamanchisathish/java-sample-application:latest" // Replace with your Docker Hub username and image name
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
            -Dsonar.projectKey=sample-java-application \
            -Dsonar.host.url=http://sonarqube.infonxt.com:9000 \
            -Dsonar.login=fecd2bcf1943684466bac09c5767b8f202b549cb"
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
		
		stage('Docker image scanner') {
            steps {
                script {
                    // Scan  Docker Image
                   sh "trivy image --exit-code 0 --no-progress ${IMAGE_TAG}"
				   echo "Image scanning Successfully by using Trivy"
                }
            }
        }
		
		stage('Image Push to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub
                    sh "echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login --username ${DOCKERHUB_CREDENTIALS_USR} --password-stdin"
                    // Pushing Image to Docker Hub
                    sh "docker push ${IMAGE_TAG}"
					echo "Successfully Push the Image to DockerHub"
                }
            }
        }
    }
}


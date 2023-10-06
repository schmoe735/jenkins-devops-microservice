pipeline {
	// agent any
	agent { docker { image 'openjdk:8-jdk-alpine' }}
	environment {
		dockerHome = tool 'dockerjenkins'
		mavenHome = tool  'mvnjenkins'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps {
				// sh "java --version"
				sh "mvn --version"
				sh "docker version"

				echo "Build Step"
				echo "$PATH"
				echo "BUILD NUMBER - $env.BUILD_NUMBER"
				echo "BUILD ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}
		stage('Compine') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage('Build docker image') {
			steps {
				// docker build -t tombanco83/currency-exchange-devops:$env.BUILD_TAG
				script {
					dockerImage = docker.build("tombanco83/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}

		}
		stage('Push Docker image') {
			steps {
				script {
					docker.withRegistry('', 'dockerhub') {
						dockerImage.push()
						dockerImage.push('latest')
					}
				}
			}
		}
	}
	post {
		always {
			echo 'I run always'
		}
		success {
			echo 'I run when successful'
		}
		failure {
			echo 'I run when the build fails'
		}
	}
}

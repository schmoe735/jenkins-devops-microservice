pipeline {
	agent any
	// agent { docker {image 'maven:3.6.3'}}
	stages {
		stage('Build') {
			steps {
				// sh "mvn --version"
				echo "Build Step"
				echo "$PATH"
				echo "BUILD NUMBER - $env.BUILD_NUMBER"
				echo "BUILD ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}
		stage('Test') {
			steps {
				echo "Test Step"
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test Step"
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

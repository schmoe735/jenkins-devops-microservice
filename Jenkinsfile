pipeline {
	agent { docker {image 'maven:3.6.3'}}
	stages {
		stage('Build') {
			steps {
				sh "mvn --version"
				echo "Build Step"
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

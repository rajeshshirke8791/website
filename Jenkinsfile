pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-rajesh')
	}

	stages {

		stage('Build') {

			steps {
				sh 'docker build /home/ubuntu/jenkins/workspace/job2/. it img2'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push rajeshshirke/ig2:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}

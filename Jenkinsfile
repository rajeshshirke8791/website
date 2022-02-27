pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub-rajesh')
	}

	stages {

		stage('Build') {

			steps {
				sh 'sudo docker build /home/ubuntu/jenkins/workspace/job2/. -t img2'
			}
		}

		stage('Login') {

			steps {
				sh 'sudo echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'sudo docker push rajeshshirke/ig2:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}

pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('rajesh-dockerhub')
	}

	stages {

                stage('gitclone') {

                        steps {
                                sh 'git clone https://github.com/rajeshshirke8791/website.git'
                        }
                }

		stage('Build') {

			steps {
				sh 'sudo docker build -t rajeshshirke/img2:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'sudo echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'sudo docker push rajeshshirke/img2:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}

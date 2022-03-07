pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('rajesh-dockerhub')
	}

	stages {

		stage('Build') {

			steps {
				sh 'sudo docker build -t rajeshshirke/img2:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}


		stage('Push') {

			steps {
				sh 'sudo docker push rajeshshirke/img2:latest'
			}
		}


		stage('Deploy to K8s')
		{
			steps {
				 /*sh 'ssh ubuntu@3.86.197.38 kubectl apply -f /home/ubuntu/website/deployment.yaml --kubeconfig=/home/.kube/config/kube.yaml'*/
				 sh 'kubectl apply -f /home/ubuntu/jenkins/workspace/job5/deployment.yaml'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}

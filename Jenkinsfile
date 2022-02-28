pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('rajesh-dockerhub')
	}

	stages {

		/*stage('Build') {

			steps {
				sh 'docker build -t rajeshshirke/img2:latest .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}


		stage('Push') {

			steps {
				sh 'docker push rajeshshirke/img2:latest'
			}
		}*/


		stage('Deploy to K8s')
		{
			steps{
				sshagent(['rajesh-k8'])
				{
					sh 'scp -r -o StrictHostKeyChecking=no deployment.yaml ubuntu@172.31.85.244:/home/ubuntu/website'
					
					script{
						try{
							sh 'ssh ubuntu@172.31.85.244 kubectl apply -f /home/ubuntu/website/deployment.yaml --kubeconfig=/home/.kube/config/kube.yaml'

							}catch(error)
							{

							}
					}
				}
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}

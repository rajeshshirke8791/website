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
                                        script{
                                                try{
                                                        /*sh 'kubectl apply -f /home/ubuntu/jenkins/workspace/job5/deployment.yaml'*/
							kubernetesDeploy(Configs: "deployment.yaml" kubeconfigId: "kubernetes")
                                                        }catch(error)
                                                        {

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

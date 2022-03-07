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
				sshagent(credentials:['rajesh-k8jenkins'])
                                {
                                        sh 'scp -r -o StrictHostKeyChecking=no deployment.yaml ubuntu@54.164.124.87:/home/ubuntu/jenkins/workspace/job5'

                                        script{
                                                try{
                                                        sh 'ssh ubuntu@54.164.124.87 kubectl apply -f /home/ubuntu/jenkins/workspace/job5/deployment.yaml'

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

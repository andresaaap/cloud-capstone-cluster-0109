pipeline {
	agent any
	stages {
		stage('Create blue kubernetes cluster') {
			steps {

				sh '''
					eksctl create cluster \
					--name bluecluster0109 \
					--version 1.13 \
					--nodegroup-name standard-workers \
					--node-type t2.micro \
					--nodes 1 \
					--nodes-min 1 \
					--nodes-max 4 \
					--node-ami auto
				'''
				
			}
		}

		stage('Create green kubernetes cluster') {
			steps {
				
					sh '''
						eksctl create cluster \
						--name greencluster0109 \
						--version 1.13 \
						--nodegroup-name standard-workers \
						--node-type t2.micro \
						--nodes 1 \
						--nodes-min 1 \
						--nodes-max 4 \
						--node-ami auto
					'''
				
			}
		}

		stage('Create conf file cluster blue') {
			steps {
				
					sh '''
						aws eks --region us-east-1 update-kubeconfig --name bluecluster0109
					'''
				
			}
		}

		stage('Create conf file cluster green') {
			steps {
				
					sh '''
						aws eks --region us-east-1 update-kubeconfig --name greencluster0109
					'''
				
			}
		}
	}
}
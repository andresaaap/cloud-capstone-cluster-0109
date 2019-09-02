

pipeline {
	agent any
	stages {
		stage('Create blue kubernetes cluster') {
			steps {
				withAWS(region:'us-east-1', credentials:'aws-static') {
					sh '''
						aws configure list
						eksctl create cluster \
						--name bluecluster0109 \
						--version 1.13 \
						--nodegroup-name standard-workers \
						--node-type t2.micro \
						--nodes 1 \
						--nodes-min 1 \
						--nodes-max 4 \
						--node-ami auto \
						--region us-east-1
					'''
				}
			}
		}

		stage('Create green kubernetes cluster') {
			steps {
				withAWS(region:'us-east-1', credentials:'aws-static') {
					sh '''
						eksctl create cluster \
						--name greencluster0109 \
						--version 1.13 \
						--nodegroup-name standard-workers \
						--node-type t2.micro \
						--nodes 1 \
						--nodes-min 1 \
						--nodes-max 4 \
						--node-ami auto \
						--region us-east-1
					'''
				}
			}
		}

		stage('Create conf file cluster blue') {
			steps {
				withAWS(region:'us-east-1', credentials:'aws-static') {
					sh '''
						aws eks --region us-east-1 update-kubeconfig --name prodalvima2
					'''
				}
			}
		}

		stage('Create conf file cluster green') {
			steps {
				withAWS(region:'us-east-1', credentials:'aws-static') {
					sh '''
						aws eks --region us-east-1 update-kubeconfig --name prodalvimagreen
					'''
				}
			}
		}
	}
}
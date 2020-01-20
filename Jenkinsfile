node{
	stage('Poll') {
		checkout scm
	}
	stage('Build Docker image'){
           
	     sh 'ansible-playbook /opt/k8s-lab/create-simple-devops-image.yml'

          }

}

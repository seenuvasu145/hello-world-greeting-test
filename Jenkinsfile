node{
	stage('Poll') {
		checkout scm
	}
	stage('Build Docker image'){
           
	     sh 'ansible-playbook /opt/k8s-lab/create-simple-devops-image.yml'

          }
        stage('Push Docker image'){

            withCredentials([string(credentialsId: 'docker-pwd', variable: 'Dockerhubpwd')]) {

            sh " docker login -u vasucena145 -p ${Dockerhubpwd}"

         }

           sh 'docker push vasucena145/simple-devops-image'

           sh 'docker rmi simple-devops-image:latest vasucena145/simple-devops-image -f'

        }
}

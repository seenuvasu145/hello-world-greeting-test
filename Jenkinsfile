node {
	stage('Poll') {
		checkout scm
	}
//	stage('Build & Unit test'){
//		sh 'mvn clean verify -DskipITs=true';
//      		junit '**/target/surefire-reports/TEST-*.xml'
//      		archive 'target/*.war'
//   	}
//	stage('Static Code Analysis'){
//   		sh 'mvn clean verify sonar:sonar -Dsonar.host.url=http://192.168.0.203:9000 -Dsonar.projectName=kubernetes-project -Dsonar.projectKey=kubernetes-project -Dsonar.projectVersion=$BUILD_NUMBER';
//	}
//	stage ('Integration Test'){
  //  		sh 'mvn clean verify -Dsurefire.skip=true';
  //       	junit '**/target/failsafe-reports/TEST-*.xml'
  //    		archive 'target/*.war'
  //	}
  //      stage ('Publish'){
  //  		def server = Artifactory.server 'Default Artifactory Server'
  //  		def uploadSpec = """{
  //  		"files": [
  //  		{
  //   		"pattern": "target/Esafe-0.0.1.war",
  //   		"target": "kubernetes-project/${BUILD_NUMBER}/",
  //	 	"props": "Integration-Tested=Yes;Performance-Tested=No"
  // 		}
  //       	]
  //		}"""
//		server.upload(uploadSpec)
//	}
//	stash includes: 'target/Esafe-0.0.1.war,src/pt/Hello_World_Test_Plan.jmx', name: 'binary'


  //     stage ('Start Tomcat'){
  //  		sh label: '', script: '''cd /home/jenkins/tomcat/bin
  //  		./startup.sh''';
  //	}
  //	stage ('Deploy '){
  //  		unstash 'binary'
  //  		sh 'cp target/Esafe-0.0.1.war /home/jenkins/tomcat/webapps/';
  //	}
  //	stage ('Performance Testing'){
  //  		sh '''cd /opt/jmeter/bin/
  //  		./jmeter.sh -n -t $WORKSPACE/src/pt/Hello_World_Test_Plan.jmx -l $WORKSPACE/test_report.jtl''';
  //		step([$class: 'ArtifactArchiver', artifacts: '**/*.jtl'])
  //	}
  //      stage ('Promote build in Artifactory'){
  //  		withCredentials([usernameColonPassword(credentialsId: 'artifactory-account', variable: 'credentials')]) {
  //  			sh 'curl -u${credentials} -X PUT "http://192.168.0.203:8081/artifactory/api/storage/kubernetes-project/${BUILD_NUMBER}/Esafe-0.0.1.war?properties=Performance-Tested=Yes"';
//		}
//	}
//	stage('Deploy to ansiblesaerver'){
//             def server = Artifactory.server 'Default Artifactory Server'
//             def downloadSpec = """{
//             "files": [
//              {
//              "pattern": "kubernetes-project/$BUILD_NUMBER/*.war",
//              "target": "/opt/k8s-lab/",
//              "props": "Performance-Tested=Yes;Integration-Tested=Yes",
//              "flat": "true"
//               }
//               ]
//               }"""
//               server.download(downloadSpec)
 //              }
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

node {
	stage('Poll') {
		checkout scm
	}
	stage('Build & Unit test'){
		sh 'mvn clean verify -DskipITs=true';
      		junit '**/target/surefire-reports/TEST-*.xml'
      		archive 'target/*.war'
   	}
	stage('Static Code Analysis'){
    		sh 'mvn clean verify sonar:sonar -Dsonar.host.url=http://192.168.0.203:9000 -Dsonar.projectName=kubernetes-project -Dsonar.projectKey=kubernetes-project -Dsonar.projectVersion=$BUILD_NUMBER';
	}
	stage ('Integration Test'){
    		sh 'mvn clean verify -Dsurefire.skip=true';
		junit '**/target/failsafe-reports/TEST-*.xml'
      		archive 'target/*.war'
	}
}

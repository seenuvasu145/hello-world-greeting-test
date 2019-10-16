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
    		sh 'mvn clean verify sonar:sonar -Dsonar.projectName=kubernetes-project -Dsonar.projectKey=kubernetes-project -Dsonar.projectVersion=$BUILD_NUMBER';
	}
}

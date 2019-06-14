pipeline {
    agent any
	tools {
		maven 'maven_3_6_1'
	}
    stages {
	    stage('Initialize Stage') {
            steps {
				echo '***** INITIALIZE STAGE *****'
				sh 'mvn clean'
            }
        }
        stage('Build Stage') {
            steps {
				echo '***** BUILD STAGE **********'
				sh 'mvn compile'
				sh 'mvn package'
            }
        }
        stage('Testing Stage') {
            steps {
				echo '***** TEST RESULTS ********'
      				junit '**/target/surefire-reports/TEST-*.xml'
      				archiveArtifacts 'target/*.war'
            }
        }
        stage('Quality Stage') {
            steps {
				echo '***** CODE QUALITY ********'
				sh 'mvn sonar:sonar'
            }
        }
    }
}

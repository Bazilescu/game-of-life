pipeline {
	agent any 
		stages {

			stage('Build') {
				steps {
					sh 'mvn clean verify -DskipTests'
				}
				
			}
			stage('Release') {
				steps {
					sh 'mvn clean -s settings.xml --batch-mode release:clean release:prepare release:perform'
				}
			}
				
			stage('Deploy Nexus') {
				steps {
					sh 'mvn clean -s settings.xml deploy -U -Dmaven.test.skip=true'
				}
			}	
	
		}
	}
}

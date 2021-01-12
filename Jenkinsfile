pipeline {
	agent any 
		stages {
			stage('Install Nexus') {
				steps {
					sh '''
						cd /opt
						wget http://download.sonatype.com/nexus/3/nexus-3.22.0-02-unix.tar.gz
						tar -xvf nexus-3.22.0-02-unix.tar.gz
						mv nexus-3.22.0-02 nexus
					
					'''
				}	
			}		
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

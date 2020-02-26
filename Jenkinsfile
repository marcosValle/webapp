pipeline{
	agent any
	tools{
		maven 'maven'
	}
	stages{
		stage('Initialize'){
			steps{
				sh '''
					echo "PATH = ${PATH}"
					echo "M2_HOME = ${M2_HOME}"
				   '''
			}
		}
		
		stage('Build'){
			steps{
				sh 'mvn clean package'
			}
		}
		
		stage('Deploy-To-Tomcat'){
			steps{
				sshagent(['tomcat']){
					sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@18.228.22.233:/opt/tomcat/webapps/webapp.war'
				}
			}
		}
		
		
	}

}

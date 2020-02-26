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
		
		stage('Check-Git-Secrets'){
			steps{
				sh 'rm trufflehog || true'
				sh 'docker pull gesellix/trufflehog'
				sh 'docker run -t gesellix/trufflehog --json https://github.com/marcosValle/webapp.git > trufflehog'
				sh 'cat trufflehog'
			}
		}
		
		stage('Source-Composition-Analysis'){
			steps{
				sh 'rm owasp || true'
				sh 'wget https://raw.githubusercontent.com/marcosValle/webapp/master/owasp-dependency-check.sh'
				sh 'chmod +x owasp-dependency-check.sh'
				sh 'bash owasp-dependency-check.sh'
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

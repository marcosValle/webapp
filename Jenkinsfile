pipeline{
	agent any
	tools{
		maven 'apache-maven-3.0.1'
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
				sh 'mvn clean packages'
			}
		}
	}

}

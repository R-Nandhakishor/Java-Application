pipeline{
	agent{
		node{
			label 'maven'
		}
	} 
	environment{
		PATH ="/opt/apache-maven-3.9.4/bin:$PATH"
	}
	stages{

		stage ('build'){
			steps{
			  echo "------------build stareted--------"	
			  sh 'mvn clean deploy -Dmaven.test.skip=true'
			  echo "------------build completed--------"	
			}
		}

		stage ('test'){
			steps{
			  echo "------------unit test stareted--------"	
			  sh 'mvn surefire-report:report'
			  echo "------------unit test completed--------"	
			}
		}
		stage ('SonarQube analysis'){
			environment {
				scannerHome= tool 'kishor-sonar-scanner'
			} 
			steps{
				withSonarQubeEnv('kishor-sonarqube-server'){
					sh "${scannerHome}/bin/sonar-scanner"
				}
			} 
		}
	}	
}
	

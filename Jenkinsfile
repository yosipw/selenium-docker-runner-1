pipeline{
	agent any
	stages{ 
		stage('delete files from workspace') {
		  steps {
		    sh 'whoami'
		  }
		}
		stage("Pull Latest Image"){
			steps{
				sh "docker pull yosua161/selenium-docker"
			}
		}
		stage("Start Grid"){
			steps{
				sh "docker-compose up -d hub chrome firefox"
			}
		}
		stage("Run Test"){
			steps{
				sh "docker-compose up book-flight-module"
			}
		}
	}
	post{
		always{
			archiveArtifacts artifacts: 'output/**'
			sh "docker-compose down"
	        cucumber buildStatus: 'UNSTABLE',
	                failedFeaturesNumber: 1,
	                failedScenariosNumber: 1,
	                skippedStepsNumber: 1,
	                failedStepsNumber: 1,
	                fileIncludePattern: '**/*cucumber-report.json',
	                sortingMethod: 'ALPHABETICAL',
	                trendsLimit: 100
		}
	}
}
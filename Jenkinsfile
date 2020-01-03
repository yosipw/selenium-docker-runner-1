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
	    stage('Generate HTML report') {
	        cucumber buildStatus: 'UNSTABLE',
	                fileIncludePattern: '**/*.json',
	                trendsLimit: 10,
	                classifications: [
	                    [
	                        'key': 'Browser',
	                        'value': 'Firefox'
	                    ]
	                ]
	    }
	}
	post{
		always{
			archiveArtifacts artifacts: 'output/**'
			sh "docker-compose down"
		}
	}
}
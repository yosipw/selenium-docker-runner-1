pipeline{
	agent any
	stages{
		stage("Pull Latest Image"){
			steps{
				sh "sudo docker pull yosua161/selenium-docker"
			}
		}
		stage("Start Grid"){
			steps{
				sh "sudo docker-compose up -d hub chrome firefox"
			}
		}
		stage("Run Test"){
			steps{
				sh "sudo docker-compose up book-flight-module"
			}
		}
	}
	post{
		always{
			archiveArtifacts artifacts: 'output/**'
			sh "sudo docker-compose down"
			sh "sudo rm -rf output/"
		}
	}
}
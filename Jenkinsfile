pipeline{
	agent any
	stages{
	//here we are pulling the latest image from the repo
	//otherwise if you don't pull, docker will always use the local image it had pulled initially for all the tests
		stage("Pull Latest Image"){
			steps{
				bat "docker pull roronoazorroippo/selenium-docker"
			}
		}
	//Here we run the grid seperately
	//using the -d command we run it in the background
	//And only select the Hub, Chrome, and Firefox images to run from the docker-compose file	
		stage("Start Grid"){
			steps{
				bat "docker-compose up -d hub chrome firefox"
			}
		}
	//We then run the test images seperately 
		stage("Run Test"){
			steps{
				bat "docker-compose up search-module book-flight-module"
			}
		}
	}
	//This post command always runs even if we kill the job.
	//Here we are saying to archive the test results in the slaves workspace directory
	
	post{
		always{
			bat "docker-compose down" //we put the down command here so even if we kill the job the grid will be brought down successfully
		}
	}
}

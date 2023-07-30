currentBuild.description = "branchName: ${env.branchName}"
pipeline {
	agent { label 'build01'}
	options { skipDefaultCheckout true }
	stages {
		stage("CheckOut"){
			steps {
				script{
					checkout([$class: 'GitSCM', 
							   branches: [[name: "${env.branchName}"]], 
							   extensions: [], 
							   userRemoteConfigs: [[
				   			   		credentialsId: '9d02cccf-5f45-46d6-b4e5-81ff97809c12', 
				   			   		url: "${env.srcUrl}"]]])

				}
			}
		}

		stage("Build"){
			steps {
				script{


				}
			}

		}

		stage("Test"){
			when {
			  environment name: 'skipUnitTest', value: 'false'
			}			
			steps{
				script{
					sh "gradle test"

				}
			}
		}

	}
}



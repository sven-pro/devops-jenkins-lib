//加载共享库
@Library("devops") _

//引用共享库
def build = new org.devops.Build()

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
					//调用共享库中的build方法
					build.Build()
				}
			}
		}

		stage("Test"){
			when {
			  environment name: 'skipUnitTest', value: 'false'
			}			
			steps{
				script{
					//调用共享库中的test方法
					build.UnitTest()
				}
			}
		}

	}
}



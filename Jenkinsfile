// Scripted
// node {
	
// 		echo "Build"
// 	    echo "Test"
// 		echo "Integration Test"
// }


// Declarative
pipeline {
	agent any
    //agent { docker { image 'maven:3.9.4' } }
	environment{
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage('Checkout'){
			steps{
				//sh 'mvn --version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
			}
		}
		stage('Compile'){
			steps{
			sh "mvn clean compile"
		}
		}
		stage('Test'){
			steps{
				sh "mvn test"
			}
		}
		stage('Integration Test'){	
			steps{
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		stage('Build Docker Image'){
			steps{
			   script{
				docker.build("in28min/currency-exchange-devops:${env.BUILD_TAG}")
			}
		}
		}
		stage('Push Docker Image'){
			steps{
			   script{
				docker.withRegistry('','dockerhub')
				dockerImage.push();
				dockerImage.push('latest');
			}
			}
		}
		stage('Package'){	
			steps{
				sh "mvn package -DskipTests"
			}
		}
	}

	post{
		always {
			echo 'Im awesome.I run always'
		}
		success {
			echo 'I run when you are success'
		}
		failure {
			echo 'I run when u fail'
		}

	}

}
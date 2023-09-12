// Scripted
node {
	
		echo "Build"
	    echo "Test"
		echo "Integration Test"
}


// Declarative
pipeline {
	agent any
	stages{
		stage('Build'){
			steps{
				echo "Build"
			}
		}
	}

	stages{
		stage('Test'){
			steps{
				echo "Test"
			}
		}
	}

	stages{
		stage('Integration Test'){
			steps{
				echo "Integration Test"
			}
		}
	}

}
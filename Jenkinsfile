pipeline {
  agent any

  stages {
    stage("Prepare Environment") {
      steps {
        echo "Download buildscipts"
        echo "Check availability of tools"
      }
    }
    stage("Check artefact cache") {
      steps {
        echo "Check cache or check rebuild"
      }
    }
    stage("Integrate") {
      steps {
        echo "Integrate"
        echo "upload to artefact cache"
      }
    }
    stage("Test") {
      steps {
        lock(resource: 'selenium-cluster'){
          echo "testtesttest"
        }
      }
    }
    stage("Populate artefact cache") {
      steps {
        echo "upload to artefact cache"
      }
    }
    stage("Confirm") {
//	when {
//		branch: 'production'
//	}
	steps {
		echo "Notify about readyness to deploy"
		input message: "Confirm?"
		milestone 2
	}
    }
//#    stage("Deploy") {
//#      when { anyOf { branch 'deploy/production'; branch 'deploy/staging' } }
//#      steps {
//#        milestone 3
//#        input message: "Proceed?"
//#        milestone 4
//#
//#        echo "deploying"
//#      }
//#    }
    stage("Generate reports") {
      steps {
        echo "Collect logs"
        echo "generate reports"
        echo "send mails"
      }
    }
  }
}

@Library('de.monkz.jenkins-shared-libs@master') _

pipeline {
  agent any
  stages {
    stage('Prepare Environment') {
      steps {
        echo 'Download buildscipts'
        echo 'Check availability of tools'
      }
    }
    stage('Check artefact cache') {
      steps {
        echo 'iCheck cache or check rebuild!'
      }
    }
    stage('Integrate') {
      steps {
        echo 'Integrate'
        echo 'upload to artefact cache'
      }
    }
    stage('Test') {
      steps {
        lock(resource: 'selenium-cluster') {
          echo 'testtesttest'
	  sleep 20
        }
        
      }
    }
    stage('Populate artefact cache') {
      steps {
	milestone 1
        echo 'upload to artefact cache'
	sleep 10
      }
    }
    stage('Confirm') {
      when {
        branch 'deploy/production'
      }
      steps {
	milestone 2
	sleep 30
        milestone 3
	sh '/usr/bin/env'
        cancelOlderBuildsAfterMilestone()
        echo 'Notify about readyness to deploy'
        input 'Confirm?'
        milestone 4
      }
    }
    stage('Deploy') {
      when {
        anyOf {
          branch 'deploy/production'
          branch 'deploy/staging'
        }
        
      }
      steps {
        milestone 5
        input 'Proceed?'
        milestone 6
        echo 'deploying'
      }
    }
    stage('Generate reports') {
      steps {
        echo 'Collect logs'
        echo 'generate reports'
        echo 'send mails'
      }
    }
  }
}

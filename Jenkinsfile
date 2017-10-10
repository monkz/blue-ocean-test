@Library('de.monkz.jenkins-shared-libs@master') _

pipeline {
  agent none
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
        }
        
      }
    }
    stage('Populate artefact cache') {
      steps {
        echo 'upload to artefact cache'
      }
    }
    stage('Confirm') {
      when {
        branch 'deploy/production'
      }
      steps {
        milestone 2
        cancelOlderBuildsAfterMilestone
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

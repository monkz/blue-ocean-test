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
        script {
          def jobname = env.JOB_NAME
          def buildnum = env.BUILD_NUMBER.toInteger()
          def job = Jenkins.instance.getItemByFullName(jobname)
          for (build in job.builds) {
            if (!build.isBuilding()) { continue; }
            if (buildnum == build.getNumber().toInteger()) { continue; println "equals" }
            build.doStop();
          }
        }
        
        echo 'Notify about readyness to deploy'
        input 'Confirm?'
        milestone 4
        node(label: 'any') {
          sh 'echo subnode'
        }
        
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
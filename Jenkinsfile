pipeline {
  agent any

  options {
    ansiColor('xterm')
  }

  parameters {
    choice(name: 'ENV', choices: ['', 'dev', 'prod'], description: '')
    choice(name: 'COMPONENT', choices: ['shipping'], description: '')
    string(name: 'APP_VERSION', defaultValue: '', description: 'APP_VERSION')
  }

  stages {
    stage('terraform') {
      steps {
        sh '''
          terraform init
//          terraform apply -auto-approve -var ENV=${ENV} -var COMPONENT=${COMPONENT} parallelism=1
          terraform apply -auto-approve -var ENV=${ENV} -var COMPONENT=${COMPONENT} -var APP_VERSION=${APP_VERSION}
        '''
        }
      }
    }
  post {
    always {
      cleanWs ()
      }
    }
  }

// parallelism = 1 or all, to deploy content to  all instances of one component at a time or one after one.
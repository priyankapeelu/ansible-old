pipeline {
  agent any

  options {
    ansicolor('xterm')
  }

  environment {
    SSH = credentials('SSH')
  }

  stages {


    stage('do a dry run') {
      steps {
        sh '''
          ansible-playbook roboshop-check.yml -e role_name=frontend -e ansible_user=${SSH_USR} -e ansible_password=DevOps321 -e ENV-sandbox
        '''
      }
    }

  }

}

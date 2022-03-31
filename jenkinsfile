pipeline {
  agent any


  stages {


    stage('do a dry run') {
      steps {
        sh '''
          export ANSIBLE_ALLOW_WORLD_READABLE TMPFILES=true
          ansible-playbook roboshop.yml -e HOST=localhost -e role_name=frontend -c
        '''
      }
    }

  }

}

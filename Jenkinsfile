pipeline {
  agent any

  options {
    ansiColor('xterm')
  }

  environment {
    SSH = credentials('SSH')
  }

  stages {
//here we are hardcoding role_name as frontend as for demo purpose, But we need to understand which role has been really modified and we need nad we need to parse
//role name, We can get that information from git commands, Here git diff HEAD@{1} --name-only | grep roles | awk -F / '{print $2}'
   stage('do a dry run') {
      steps {
        sh '''
          ansible-playbook roboshop-check.yml -e role_name=frontend -e ansible_user=${SSH_USR} -e ansible_password=DevOps321 -e ENV-sandbox -e CHECK_MODE=true
        '''
      }
    }

  }

}

pipeline {
  agent any

  options {
    ansiColor('xterm')
  }

  environment {
    SSH = credentials('SSH')
  }

  stages {

   stage ( 'check ansible style checks' ) {
   when { branch pattern: "ROB-.*", comparator: "REGEXP"}
        steps {
         echo "ansible style checks"
         // we will find the right tool.
        }
     }

     stage ( 'run ansible in sandbox envirnonment' ) {
       when { branch pattern: "PR-.*", comparator: "REGEXP"}
        steps {
           sh '''
             ansible-playbook roboshop-check.yml -e role_name=frontend -e ansible_user=${SSH_USR} -e ansible_password=${SSH_PSW} -e ENV=sandbox -e CHECK_MODE=true
             '''
           }
        }

      stage ('promote code to PROD branch') {
           when { branch 'main' }
             steps {
                sh 'env'
                sh 'echo MAIN'
                }
           }
     }
}



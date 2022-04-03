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

//here we are hardcoding role_name as frontend as for demo purpose, But we need to understand which role has been really modified and we need nad we need to parse
//role name, We can get that information from git commands, Here git diff HEAD@{1} --name-only | grep roles | awk -F / '{print $2}'
//    stage('do a dry run') {
//       steps {
//         sh '''
//         env
//           ansible-playbook roboshop-check.yml -e role_name=frontend -e ansible_user=${SSH_USR} -e ansible_password=DevOps321 -e ENV-sandbox -e CHECK_MODE=true
//         '''
//       }
//     }
//
//   }
//
// }

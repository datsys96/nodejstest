pipeline {
     agent { label 'jenkinslave1' }
     stages {
          stage("clone code") {
               steps {
                    git 'https://github.com/datsys96/nodejstest.git'
               }
          }
          stage("test code") {
               steps {
                    sh 'npm install'
                    sh 'nohup node index.js &'
                    sh 'npm test'
               }
          }
	  stage("test junit") {
               steps {
                    junit 'test.xml'
               }
          }
     }
    post {
        always {
        emailext body: 'helle day la jenkin nha', subject: 'test jenkin', to: 'datbeo12c@gmail.com'
        }
        success {
	    sh 'docker build -t nodejstest:1 .'
            emailext body: 'ok ${DEFAULT_SUBJECT}', subject: '${DEFAULT_CONTENT}', to: 'datbeo12c@gmail.com'
        }
        unstable {
            emailext body: 'unstable ${DEFAULT_SUBJECT}', subject: '${DEFAULT_CONTENT}', to: 'datbeo12c@gmail.com'
        }
        failure {
            emailext body: 'failure ${DEFAULT_SUBJECT}', subject: '${DEFAULT_CONTENT}', to: '$datbeo12c@gmail.com'
        }
        changed {
            emailext body: 'change ${DEFAULT_SUBJECT}', subject: '${DEFAULT_CONTENT}', to: 'datbeo12c@gmail.com'
        }
    }

}

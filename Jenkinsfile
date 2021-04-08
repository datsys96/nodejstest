pipeline {
     agent { label 'jenkinslave1' }
     environment {
        scannerHome = tool 'sonarscan’
     }
     stages {
          stage("clone code") {
               steps {
                    git 'https://github.com/datsys96/nodejstest.git'
               }
          }
	   stage("sona scaner") {
               steps {
               withSonarQubeEnv('sonar') {
		sh "${scannerHome}/bin/sonar-scanner"     
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
        emailext body: 'helle day la jenkin nha', subject: 'test jenkin', to: 'tuandatithubt@gmail.com'
        }
        success {
	    sh 'docker build -t nodejstest:1 .'
            emailext body: 'ok ${DEFAULT_SUBJECT}', subject: '${DEFAULT_CONTENT}', to: 'tuandatithubt@gmail.com'
        }
        unstable {
            emailext body: 'unstable ${DEFAULT_SUBJECT}', subject: '${DEFAULT_CONTENT}', to: 'tuandatithubt@gmail.com'
        }
        failure {
            emailext body: 'failure ${DEFAULT_SUBJECT}', subject: '${DEFAULT_CONTENT}', to: '$tuandatithubt@gmail.com'
        }
        changed {
            emailext body: 'change ${DEFAULT_SUBJECT}', subject: '${DEFAULT_CONTENT}', to: 'tuandatithubt@gmail.com'
        }
    }

}

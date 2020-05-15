pipeline {
  agent {
  docker { image 'gesellix/trufflehog' }
  }
  tools {
   maven 'Maven'
   }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    
    stage ('Check-Git-Secrets') {
      steps {
        bash  service docker start
        sh 'rm trufflehog || true'
        sh 'docker run gesellix/trufflehog --json https://github.com/cehkunal/webapp.git > trufflehog'
        sh 'cat trufflehog'
      }
    }
      stage ('Build') {
         steps {
         sh 'mvn clean package'
       }
      }
    }
  }

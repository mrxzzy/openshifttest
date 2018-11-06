pipeline {
  agent {
    node {
      label 'jenkins-slave-gcc'
    }
  }

  stages {
    stage('build') {
      steps {
        script {
          openshift.withCluster(){
            openshift.withProject(){
              echo 'running build'
              sh './build.sh'
            }
          }
        }
      }
    }
    stage('test') {
      steps {
        script {
          openshift.withCluster(){
            openshift.withProject(){
              echo 'testing...'
              sh './test.sh'
            }
          }
        }
      }
    }
    stage('deploy') {
      steps {
        script {
          openshift.withCluster(){
            openshift.withProject(){
              archiveArtifacts artifacts: 'build.log', onlyIfSuccessful: true
            }
          }
        }
      }
    }
  }
}

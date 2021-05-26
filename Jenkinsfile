pipeline {
  agent none
  tools { 
        maven 'Maven 3.8.1' 
        }
  stages {
    stage('Build & Test') {
      agent any
      steps {
        sh 'mvn -Dmaven.test.failure.ignore clean package'
        stash(name: 'build-test-artifacts', includes: '**/ target/surefire-reports/TEST-*.xml,target/*.jar')
      }
    }

    stage('Report & Publish') {
      agent any
      steps {
        unstash 'build-test-artifacts'
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts(artifacts: 'target/*.jar', onlyIfSuccessful: true)
      }
    }

  }
}

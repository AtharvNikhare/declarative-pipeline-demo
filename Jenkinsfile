pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Run build'
      }
    }

    // Use nested stages so we can run preparation steps and then run parallel test stages
    stage('Test') {
      stages {
        stage('Prepare') {
          steps {
            sh 'chmod a+x run_build_script.sh'
            sh './run_build_script.sh'
          }
        }

        stage('Parallel Tests') {
          parallel {
            stage('Test On Windows') {
              steps {
                echo 'Running tests on Windows'
              }
            }
            stage('Test On Linux') {
              steps {
                echo 'Running tests on Linux'
              }
            }
          }
        }
      }
    }
  }
}

pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo "Run build"
      }
    }
    stage('Test') {
      steps {
       sh 'chmod a+x run_build_script.sh'
       sh './run_build_script.sh'
      }
      parallel {
      stage('Test On Windows') {
        steps {
          echo "Running tests on Windows"
        }
      }
      stage('Test On Linux') {
        steps {
          echo "Running tests on Linux"
        }
      }
    }
    }
  }
}

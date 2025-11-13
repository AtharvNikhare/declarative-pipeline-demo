pipeline {
    // You should define an agent at the top-level
    agent any 

    // Use top-level stages to define the sequence of work
    stages {
        // Stage 1: Preparation/Build
        stage('Preparation and Build') {
            steps {
                // Ensure the script is executable and run it
                sh 'chmod a+x run_build_script.sh'
                sh './run_build_script.sh'
            }
        }

        // Stage 2: Parallel Testing (runs tests simultaneously)
        stage('Parallel Tests') {
            // The stages here run in parallel
            parallel {
                stage('Test On Windows') {
                    agent { label 'windows' } // Assuming you have a Windows agent
                    steps {
                        echo "Running tests on Windows"
                        // Add actual test commands here
                    }
                }
                stage('Test On Linux') {
                    agent { label 'linux' } // Assuming you have a Linux agent
                    steps {
                        echo "Running tests on Linux"
                        // Add actual test commands here
                    }
                }
            }
        }

        // Stage 3: Deployment to Staging (requires confirmation)
        stage('Deploy to Staging') {
            steps {
                // Confirmation step
                timeout(time: 60, unit: 'SECONDS') {
                    input(message: "Okay to Deploy to Staging?", ok: "Let's Do it!")
                }
                
                // Deployment step
                echo "Deploying to staging..."
                // Add actual deployment commands here
            }
        }

        // Stage 4: Deployment to Production (requires confirmation)
        stage('Deploy to Production') {
            steps {
                // Confirmation step
                timeout(time: 60, unit: 'SECONDS') {
                    input(message: "Okay to Deploy to Production?", ok: "Let's Do it!")
                }
                
                // Deployment step
                echo "Deploying to production..."
                // Add actual deployment commands here
            }
        }
    }
}

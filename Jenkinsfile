pipeline {
    agent any

    stages {
        stage("starting") {
            steps {
                echo "This is for the beginning stage"
            }
        }

        stage("building") {
            steps {
                echo "This is for the building stage"
                // Simulate a failure for testing (comment this out in production)
                try{
                    def value = 10
                    if( value == 10){
                        echo "correct"
                    }else{ echo "erro"}
                }catch( Exception err){
                    echo "error : err"
                }
            }
        }

        stage("production") {
            steps {
                echo "This is for the production stage 1."
            }
        }
    }

    post {
        always {
            echo "This runs always"
        }

        success {
            echo "Pipeline completed successfully"
            // emailext(
            //     subject: "SUCCESS: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
            //     body: """
            //         <p>The pipeline has completed successfully.</p>
            //         <p>Build URL: ${env.BUILD_URL}</p>
            //     """,
            //     to: 'afeadetutu@gmail.com', // Replace with the recipient's email
            //     attachLog: false // No need to attach logs for success
            // )
        }

        failure {
            echo "Pipeline failed!"
            // emailext(
            //     subject: "FAILURE: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
            //     body: """
            //         <p>The pipeline failed with the following error:</p>
            //         <pre>${currentBuild.currentResult}</pre>
            //         <p>Check the build log for more details: ${env.BUILD_URL}</p>
            //     """,
            //     to: 'afeadetutu@gmail.com', // Replace with the recipient's email
            //     attachLog: true // Attach the build log for debugging
            // )
        }
    }
}
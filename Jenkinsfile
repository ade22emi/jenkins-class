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
            
                error("Stimulated build failure")
            }
        }

        stage("production") {
            steps {
                echo "This is for the production stage"
            }
        }
    }

    post {
        always {
            echo "This runs always"
        }

        success {
            echo "Pipeline completed successfully"
            emailext(
                subject: "SUCCESS: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                body: """
                    <p>The pipeline has completed successfully.</p>
                    <p>Build URL: ${env.BUILD_URL}</p>
                """,
                to: 'afeadetutu@gmail.com',
                attachLog: false 
            )
        }

        failure {
            echo "Pipeline failed!"
            emailext(
                subject: "FAILURE: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
                body: """
                    <p>The pipeline failed with the following error:</p>
                    <pre>${currentBuild.currentResult}</pre>
                    <p>Check the build log for more details: ${env.BUILD_URL}</p>
                """,
                to: 'afeadetutu@gmail.com', 
                attachLog: true 
            )
        }
    }
}
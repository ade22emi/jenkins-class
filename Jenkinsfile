pipeline {
    agent any
    stages {
        stage("starting"){
            steps{
                echo "This is for the beginning stage"
            }
        }

        stage("building"){
            steps{
                echo "This is for the building stage"
            }
        }

        stage("production"){
            steps{
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
            mail to: 'afeadetutu@gmail.com',
                 subject: "SUCCESS: Pipeline Completed",
                 body: "The pipeline has completed successfully."
        }
        failure {
            echo "Pipeline failed!"
            mail to: 'afeadetutu@gmail.com',
                 subject: "FAILURE: Pipeline failed",
                 body: "The pipeline failed. Check the logs."
        }
    }
}

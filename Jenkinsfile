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
                echo "This is for the prduction stage"
            }
    
        }
        
    }
    post{
        always {
            echo "This runs always"
        }
        success {
            echo "echo completed successfully"
            mail to: 'afeadetutu@gmail.com',
            subject: "SUCCESS: Pipelne Completed",
            body: "The pipeline has completed sucessfully."
        }
        failure{
            echo "echo Pipeline failed!"
            mail to: 'afeadetutu@gmail.com',
            subject: "FAILURE: Pipelne failed",
            body: "The pipeline failed check the logs."
        }
    }
}
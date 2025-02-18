
// pipeline {
//     agent any
//     tools {
//         nodejs "node18"
//     }
//     stages {

//         stage("Checkout out"){
//             steps{
//                 git branch: "master", 
//                 url: "https://github.com/ade22emi/jenkins-class.git"
//             }
//         }

//         stage("starting"){
//             steps{
//                 echo "This is for the starting stage"
//             }
//         }


//          stage("building"){
//             when{
//                 expression{
//                     BRANCH_NAME == "testing"
//                 }
//             }
//             steps{
        
//                 script {
//                     try {

//                         sh "npm run test | tee builder.log"

//                     }catch(Exception err){
//                         currentBuild.result = "FAILURE"
//                         sh "echo ${err} | tee builder.log"
//                         throw err
//                     }
//                 }
//             }
//         }

//          stage("production"){
//             steps{
//                 echo "This is for the prduction stage"
//             }
//         }

//     }

//       post{
//             failure{
//                 script {
//                     //def build_log = currentBuil.rawBuild.getLog(200).join("\n")
//                     // def build_log = manager.build.log
//                     def build_log = readFile("builder.log")
//                     emailext subject: "Everything FAILED",
//                             body: """
//                                     This is the default body. ${env.JOB_NAME} - ${env.BUILD_NUMBER}, 
//                                     ${env.BUILD_URL}
//                                     ----------------
//                                     ${build_log}
//                                     """,
//                             to: "afeadetutu@gmail.com"

//                 }
                
//             }

//              success{

//                     script {
//                         def build_log = readFile("builder.log")
//                         emailext subject: "Everything works fine from her",
//                         body: """
//                                 This is the default body. ${env.JOB_NAME} - ${env.BUILD_NUMBER}, 
//                                 ${env.BUILD_URL}
//                                 ----------------
//                                 ${build_log}
//                                 """,
//                         to: "afeadetutu@gmail.com"

//                     }
               
                
//             }
//         }
// }


pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')  // This retrieves the DockerHub credentials
    }
    tools {
        nodejs 'node18'  // Ensure Node.js is installed
    }
    stages {

        stage('Checkout') {
            steps {
                git branch: 'master', 
                    url: 'https://github.com/ade22emi/jenkins-class.git'
            }
        }

        stage('Starting') {
            steps {
                echo 'This is for the starting stage'
            }
        }

        stage('Login to DockerHub') {
            steps {
                script {
                    // Secure Docker login using --password-stdin method
                    sh """
                        echo \${DOCKERHUB_CREDENTIALS_PSW} | docker login -u \${DOCKERHUB_CREDENTIALS_USR} --password-stdin
                    """
                }
            }
        }

        stage('Building') {
            // when {
            //     expression {
            //         return BRANCH_NAME == 'master'  // Ensure we're on the master branch
            //     }
            }
            steps {
                // Build the Docker image
                sh 'sudo docker build -t kikelomo22/new-image:latest/jenkins .'

                script {
                    try {
                        // Run npm commands
                        sh 'npm init -y'
                        sh 'npm run test | tee another.log'  // Capture logs and run tests
                    } catch (Exception err) {
                        // Handle failure gracefully
                        currentBuild.result = 'FAILURE'
                        sh "echo ${err} | tee another.log"
                        throw err  // Re-throw error to mark build as failed
                    }
                }
            }
        }

        stage('Production') {
            steps {
                echo 'This is for the production stage'
            }
        }
    }

    post {
        failure {
            script {
                // Send email on failure with logs
                def build_log = readFile('another.log')
                emailext subject: 'Everything FAILED',
                    body: """
                    This is the default body. ${env.JOB_NAME} - ${env.BUILD_NUMBER}, 
                    ${env.BUILD_URL} 
                    ----------------
                    ${build_log}
                    """,
                    to: 'afeadetutu@gmail.com'
            }
        }

        success {
            script {
                // Send email on success with logs
                def build_log = readFile('another.log')
                emailext subject: 'Everything works fine from here',
                    body: """
                    This is the default body. ${env.JOB_NAME} - ${env.BUILD_NUMBER}, 
                    ${env.BUILD_URL}
                    ----------------
                    ${build_log}
                    """,
                    to: 'afeadetutu@gmail.com'
            }
        }
    }
}

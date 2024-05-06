pipeline{
//     agent{
//         node{
//             label "linux && java21"
//         }
//     }
    agent none

    environment{
        AUTHOR = "Bagi Hartawan"
        APP_CRED = credentials("bagih_cred_demo")
    }

//     options {
//         disableConcurrentBuilds()
//         timeout(time: 10, unit: "SECONDS")
//     }

//     parameters{
//         string(name: "USERNAME", defaultValue: "guest", description: "enter your username")
//         text(name: "DESCRIPTION", defaultValue: "", description: "tell me more about yourself")
//         booleanParam(name: "DEPLOY", defaultValue: false, description: "Deploy to Production?")
//         choice(name: "TEAM", choices: ['A021', 'A2201', 'B221'], description: "which team do you belong?")
//         password(name: "SECRET", defaultValue: "", description: "enter your password")
//     }

    triggers{
        cron(*/1 * * * *)
    }


    stages{
        stage("parameters preparation"){
            agent any
            steps{
                echo "username: ${params.USERNAME}"
                echo "description: ${params.DESCRIPTION}"
                echo "Deploy to production?: ${params.DEPLOY}"
                echo "From Team: ${params.TEAM}"
                echo "Password: ${params.SECRET}"
            }
        }

        stage("Prepare"){
            agent any

            environment{
                STAGE_AUTHOR = "Bagih"
            }

            steps{
                echo "AUTHOR: ${AUTHOR}"
                echo "Using username: ${APP_CRED_USR}"
//                 echo "Using password: ${APP_CRED_PSW}"
//                 sh 'echo Using Password: $APP_CRED_PSW'
                echo "stage author: ${STAGE_AUTHOR}"
                echo "Start JOB: ${env.JOB_NAME}"
                echo "Start Build: ${env.BUILD_NUMBER}"
                echo "On Branch: ${env.BRANCH_NAME}"
                echo "description: ${currentBuild.description}"
            }
        }

        stage("Build"){
            agent{
                node{
                    label "linux && java21"
                }
            }

            steps{
                echo "Build..."
                script{
//                     def data = [
//                         "firstName": "Bagi",
//                         "lastName": "Hartawan",
//                         "fullName": "Bagi Hartawan"
//                     ]
                    def dataJSON = readJSON(file: "data.json")
                    println(dataJSON)

                }
                sh("./mvnw clean compile test-compile")
                echo "finish build"
            }

        }
        stage("Test"){
            agent any

            steps{
                echo "Test..."
                sh("./mvnw test")
                echo "finish test"
            }
        }
        stage("Deploy"){
            agent any

            steps{
                echo "Deploy..."
            }
        }

    }

    post{
        always{
            echo "always: i will always executed by system"
        }
        success{
            echo "success: i will executed by system if its success"
        }
        failure{
            echo "failure: its failure, huu!"
        }
        cleanup{
            echo "cleanup: i will always be executed"
            echo "branch name: ${env.BRANCH_NAME}"
            echo "description: ${currentBuild.description}"
        }
    }
}
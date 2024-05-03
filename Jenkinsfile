pipeline{
//     agent{
//         node{
//             label "linux && java21"
//         }
//     }
    agent none

    stages{
        stage("Prepare"){
            agent any
            steps{
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
        }
    }
}
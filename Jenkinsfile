pipeline{
    agent{
        node{
            label "linux && java21"
        }
    }
    stages{
        stage("Build"){
            steps{
                echo "Build..."
            }
        }
        stage("Test"){
            steps{
                echo "Test..."
            }
        }
        stage("Deploy"){
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
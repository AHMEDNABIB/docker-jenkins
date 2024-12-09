pipeline {
    agent any
    environment{
        NEW_VERSION ='1.3.0'
        // SERVER_CREDENTIALS = credentials('server-credentials')
    }

    stages {
        stage("build"){
            steps{
                echo "building the application"
                echo "building version ${NEW_VERSION}"

            }
        }

        stage("test"){
            
            steps{
                echo "Testing the application"

            }
        }

        stage("deploy"){
            steps {
                echo "Deploying the application"
                // echo "deploying with ${SERVER_CREDENTIALS}"
                // sh "${SERVER_CREDENTIALS}"
                withCredentials([
                    usernamePassword(credentialsId: 'server-credentials', usernameVariable: 'USER', passwordVariable: 'PWD')
                ]) {
                    sh "echo Deploying with username ${USER} and password ${PWD}"
                }
            }
        }
    }
}
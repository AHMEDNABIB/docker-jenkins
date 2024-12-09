def gv

pipeline {
    agent any
    environment{
        NEW_VERSION ='1.3.0'
        // SERVER_CREDENTIALS = credentials('server-credentials')
    }

    stages {
        stage("init"){
            steps{
                script{
                    gv = load "script.groovy"
                }
            }
        }
        stage("build"){
            steps{
                script{
                    gv.buildApp()
                }
                

            }
        }

        stage("test"){
            
            steps{
                script{
                    gv.testApp()
                }

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
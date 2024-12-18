pipeline {
    agent any
    tools {
        maven 'maven-3.9'
    }
    stages {
        stage("build jar"){
            steps {
                script{
                    echo "building the application..."
                    sh 'mvn package'
                }
            }
        }

        stage("build image"){
            when {
                expression {
                    BRANCH_NAME == "master"
                }
            } 
            steps {
                script{
                    echo "building the application..."
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]){
                        sh 'docker build -t ahmednabib123/demo-app:jma-2.0 .'
                        sh 'echo $PASS | docker login -u $USER --password-stdin'
                        sh 'docker push ahmednabib123/demo-app:jma-2.0'
                    }
                }
            }
        }

        stage("deploy"){
            when {
                expression {
                    BRANCH_NAME == "master"
                }
            }
            steps{
                script{
                    echo "deploying the application..."
                }
            }
        }
    }
}
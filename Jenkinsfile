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
            steps {
                script{
                    echo "building the application..."
                    // withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]){
                    //     sh 'docker build -t ahmednabib123/demo-app:jma-2.0 .'
                    //     sh 'echo $PASS | docker login -u $USER --password-stdin'
                    //     sh 'docker push ahmednabib123/demo-app:jma-2.0'
                    // }
                     withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        // Fix Docker permission issues
                        sh '''
                        if ! groups | grep -q '\\bdocker\\b'; then
                            echo "Adding Jenkins user to the docker group..."
                            sudo usermod -aG docker $(whoami)
                        fi
                        '''
                        // Build and push Docker image
                        sh '''
                        docker build -t ahmednabib123/demo-app:jma-2.0 .
                        echo $PASS | docker login -u $USER --password-stdin
                        docker push ahmednabib123/demo-app:jma-2.0
                        '''
                    }
                }
            }
        }

        stage("deploy"){
            steps{
                script{
                    echo "deploying the application..."
                }
            }
        }
    }
}
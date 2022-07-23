pipeline {
    agent any
    tools {
        maven myMaven
    }
    stages {
        stage("build jar"){
            steps{
                script{
                    echo "building the application"
                    sh 'mvn package'
                }
            }
        }
        stage("build image"){
            steps{
                script{
                    echo "building the docker image"
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', passwordVariable: 'PASS', usernameVariable: 'USER' )])
                        sh 'docker build -t sid5233/myrepodocker:jma-2.0'
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push docker push sid5233/myrepodocker:jma-2.0'
                }
            }
        }
        stage("Deploy"){
            steps{
                script{
                    echo "deploying the application"
                }
            }
        }        
    }
}
pipeline{
    agent any

    environment {
        IMAGE_NAME = "todo-app"                //app_name
        CONTAINER_NAME = "todo-app-conatiner"    //container_name
    }
    triggers{
        githubPush()                //it was earlier githubpush()
    }

    stages{
        stage('clone Git repository '){
            steps{
                script{
                    git branch: 'main',
                    url: 'https://github.com/tarunchaudhary2/todoapp.git'
                }
            }
        }
        stage('remove image'){
            steps{
                script{
                    sh "docker rmi $IMAGE_NAME || true"
                }
            }
        }
        stage('stop and remove container'){
            steps{
                script{
                    sh """
                        docker stop $CONTAINER_NAME || true
                        docekr rm $CONTAINER_NAME || true
                    """
                }
            }
        }
        stage('build image'){
            steps{
                script{
                    sh "docker build . -t $IMAGE_NAME"
                }
            }
        }
        stage('run container'){
            steps{
                script{
                    sh "docekr run -d --name $CONTAINER_NAME -p 80:80 $IMAGE_NAME"
                }
            }
        }
    }

}

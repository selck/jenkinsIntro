pipeline {

    agent { dockerfile true }

    stages {

        stage ('Clone & Pack') {
            steps {
                echo 'Downloading latest code version...'
                checkout scm
            }
        }
        stage ('Lambdas Zip -> S3') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'develop') {
                        echo 'Uploading lambdas to S3...'
                    } else if (env.BRANCH_NAME == "qas"){
                        echo 'Uploading lambdas to S3...'
                    } else {
                        echo 'Not allowed by now'
                    }
                }
            }
        }
        stage ('API Update & Deploy') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'develop') {
                        echo 'Updating the API Gateway from latest swagger file'
                    } else if (env.BRANCH_NAME == "qas"){
                        echo 'Updating the API Gateway from latest swagger file'
                    } else {
                        echo 'Not allowed by now'
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
            // TODO: Cleanup step
            // docker system prune --force --all --volumes
            // sh 'docker rmi -f $(docker images -a -q)'
            // sh 'docker rm -vf $(docker ps -a -q)'
        }
        success {
            echo ':)'
        }
        failure {
            echo ':)'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
    }
}

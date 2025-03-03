// pipeline {
//     agent any

//     stages {
//         stage('Hello') {
//             steps {
//                 echo 'Hello World changes anr made me'
//             }
//         }
//     }
// }

pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "vishvajitkanase/web-app28"
    }

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Test Docker image') {
            steps {
                script {
                    docker.image(DOCKER_IMAGE).inside {
                        sh 'echo "Running tests..."'
                        // Add your test commands here
                    }
                }
            }
        }

        stage('Deploy Docker image') {
            steps {
                script {
                    sh """
                        docker stop web_app || true
                        docker rm web_app || true
                        docker run -d --name web_app -p 8080:80 $DOCKER_IMAGE
                    """
                }
            }
        }

        stage('View Logs') {
            steps {
                script {
                    sh 'docker logs web_app'
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}

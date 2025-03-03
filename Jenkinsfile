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

        stage('Pull Docker image') {
            steps {
                script {
                    sh 'docker pull vishvajitkanase/web-app28:latest'
                }
            }
        }

        stage('Test Docker image') {
            steps {
                script {
                    sh 'docker run --rm vishvajitkanase/web-app28 echo "Running tests..."'
                    // Add your test commands here
                }
            }
        }

        stage('Deploy Docker image') {
            steps {
                script {
                    sh 'docker stop web_app || true'
                    sh 'docker rm web_app || true'
                    sh 'docker run -d --name web_app -p 8080:80 vishvajitkanase/web-app28'
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

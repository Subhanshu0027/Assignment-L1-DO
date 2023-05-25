pipeline {
    agent {
        label 'node1'
    }
    stages {
        stage("Clone the repo") {
            steps {
                script {
                    if (!fileExists('Assignment-L1-DO')) {
                        sh 'git clone https://github.com/Subhanshu0027/Assignment-L1-DO.git'
                    } else {
                        echo 'Directory already exists, skipping cloning step.'
                    }
                }
            }
        }
        stage("Navigate to the docker file") {
            steps {
                dir('Assignment-L1-DO/aesthisia-demo') {
                    sh 'docker build -t subhanshu0027/myreactapp:latest .'
                }
            }
        }
        stage("Login to Dockerhub") {
            steps {
                sh 'docker login -u subhanshu0027 -p subhanshu0027@@docker'
            }
        }
        stage("Push to Dockerhub") {
            steps {
                sh 'docker push subhanshu0027/myreactapp:latest'
            }
        }
        stage("Run container from Docker image") {
            steps {
                sh 'docker run -d --name my-container subhanshu0027/myreactapp:latest'
            }
        }
    }
}

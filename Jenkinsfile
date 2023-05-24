pipeline {
    agent {
        label 'node1'
    }
    stages {
        stage("Clone the repo") {
            steps {
                sh 'git clone https://github.com/Subhanshu0027/Assignment-L1-DO.git'
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
    }
}

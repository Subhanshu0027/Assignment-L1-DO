pipeline{
    agent {
        node {
            label 'node1'
        }
    stages{
        stage("Clone the repo"){
            steps{
                sh 'git clone https://github.com/Subhanshu0027/Assignment-L1-DO.git'
            }
            
        }
        stage("Navigate to the docker file"){
            steps{
                sh 'cd /aesthisia-demo'
            }
            
        }
        stage("Build the docker file"){
            steps{
                sh 'docker build -t subhanshu0027/myreactapp:latest .'
            }
            
        }

        stage("login to Dockerhub"){
            steps{
                sh 'docker login -u subhanshu0027 -p subhanshu0027@@docker'
            }
            
        }
        stage("Push to Dockerhub"){
            steps{
                sh 'docker push subhanshu0027/myreactapp:latest'
            }
            
        }

    }
    
}
}

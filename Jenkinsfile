pipeline{
    agent any

    environment{
        container_exits = 'pycontainer'
    }
    stages{
        stage('Git Checkout'){
            steps{
                   echo 'checking out'
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'git', url: 'https://github.com/devops-sumit/python-docker-container']]])
            }
        }
    }
     stage('Build Image'){
            steps{
                script{
                    echo 'Starting Building Image'
                    sh 'docker build -t git/flaskapp:latest .'
                }
            }
        }


}
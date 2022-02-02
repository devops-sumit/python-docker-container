pipeline{
    agent any

    env{
        container_exits = 'pycontainer'
    }

    stages{
        stage('Git Checkout'){
            steps{
                    checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'git', url: 'https://github.com/devops-sumit/python-docker-container']]])
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
        stage('Stop Container'){
            steps{
                script{
                    if (sh 'docker ps -qa -f name=pycontainer'){
                        echo 'container exists stopping it ....'
                        sh 'docker stop container pycontainer'
                        echo 'klling container'
                        sh 'docker rm pycontainer'
                    }
                }
            }
        }
        stage('Start Container'){
            steps{
                script{
                    sh 'docker run -it -d --name pycontainer -p 5000:5000 git/flaskapp'
                }
            }
        }

    }
}
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
                    def containerExists = sh('docker ps -qa -f name=pycontainer', returnStdout: true) == 0
                    echo containerExists
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
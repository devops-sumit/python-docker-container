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

}
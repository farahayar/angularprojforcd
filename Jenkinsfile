pipeline {
    agent any


    stages {
        stage('pull') {
            steps {
                script{
                	checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                	userRemoteConfigs: [[url: 'https://github.com/farahayar/angularprojforcd.git']]])
                }
            }

        }
}
}

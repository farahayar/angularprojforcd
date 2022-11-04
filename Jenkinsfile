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
        
        stage('build') {
            steps {
                script{
                	sh "npm install --legacy-peer-deps"
                	sh "ansible-playbook ansible/build.yml -i ansible/inventory/host.yml "
                }
            }

        }
        
        stage('docker') {
            steps {
                script{
                	sh "ansible-playbook ansible/docker.yml -i ansible/inventory/host.yml "
                }
            }

        }
        
        stage('Login Dockerhub') {

	    steps {
	    	sh 'chmod 666 /var/run/docker.sock'
		sh 'docker login -u farahayari -p dckr_pat_NgrL9nAql4Ma9BHmiZzUXWL_yNU'
	 }
	}
        
        stage('docker-registry') {
            steps {
                script{
                	sh "ansible-playbook ansible/docker-registry.yml -i ansible/inventory/host.yml "
                }
            }

        }
}
}

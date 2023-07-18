pipeline{

    agent any

    stages{
        stage('Checkout the code'){
            steps{
                git branch: 'main', credentialsId: 'git_token', url: 'https://github.com/skmdab/create_nexus.git'
            }
        }

        stage('Creating server'){
            steps{
                sh "sh aws_create.sh"
            }
        }

        stage('Installing nexus package into server'){
            steps{
                withCredentials([file(credentialsId: 'pemfile', variable: 'PEMFILE')]) {
		   sh 'ansible-playbook installnexusserver.yaml --private-key="$PEMFILE"'
		}
            }
        }
    }
}

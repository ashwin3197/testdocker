pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('ashwin3197')
	}

	stages {
	    
	    stage('gitclone') {
			echo("gitclone")
			steps {
				 checkout scmGit(branches: [[name: '**']], extensions: [], userRemoteConfigs: [[credentialsId: 'githubToken', url: 'https://github.com/ashwin3197/testdocker.git']])
			}
		}

		stage('Build') {
			echo("Build")
			steps {
				sh 'docker build -t JenkinsdockerImage/nodeapp_test:latest .'
			}
		}

		stage('Login') {
			echo("Login")
			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'docker push JenkinsdockerImage/nodeapp_test:latest'
			}
		}
	}

	post {
		always {
			sh 'docker logout'
		}
	}

}

pipeline {
	agent any

	stages {
		stage('Build Code') {
			steps {
				echo 'Checking out repository...'
				checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/jepManalo/CompanyGradleBuild']]])
				echo 'Compiling source code...'
				bat 'gradle compileJava'
			}
		}

		stage('UI Tests') {
			steps {
				echo 'Running UI Tests...'
				script {
					try {
						bat 'gradle test'
					} finally {
						echo 'Posting Results...'
						junit '**/build/test-results/test/*.xml'
					}
				}
			}
		}

		stage('Clean Build') {
			steps {
				echo 'Cleaning last build...'
				bat 'gradle clean'
			}
		}
	}
}

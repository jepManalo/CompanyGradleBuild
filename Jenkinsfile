pipeline {
	agent any

	stages {
		stage('Build Code') {
			steps {
				echo 'Checking out repository...'
				checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/jepManalo/CompanyGradleBuild']]])
				echo 'Compiling source code...'
				withGradle {
					bat './gradlew compileJava'
				}
			}
		}

		stage('UI Tests') {
			steps {
				echo 'Running UI Tests...'
				script {
					withGradle {
						bat './gradlew test'
					}
				}
			}
		}

		stage('Post Results') {
			post {
				always {
					echo 'Posting Results...'
					junit '**/build/reports/tests/test/classes/*.xml'
				}
			}
		}
	}
}

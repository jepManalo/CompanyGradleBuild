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
// 				bat 'gradle compileJava'
			}
		}

		stage('UI Tests') {
			steps {
				echo 'Running UI Tests...'
				script {
					try {
						withGradle {
							bat './gradlew test'
						}
// 						bat 'gradle test'
					} finally {
						echo 'Posting Results...'
						junit '**/target/cucumber-report.xml'
					}
				}
			}
		}

		stage('Clean Build') {
			steps {
				echo 'Cleaning last build...'
				withGradle {
					bat './gradlew clean'
				}
// 				bat 'gradle clean'
			}
		}
	}
}

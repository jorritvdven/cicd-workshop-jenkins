pipeline {
	agent {
		any
	}

	stages {
		stage('Build') {
			steps {
                script {
                    sh './gradlew clean build -x test --no-daemon' //run a gradle task
                }
            }
		}

		stage('Test') {
			steps {
				try {
                	sh './gradlew test --no-daemon' //run a gradle task
                } finally {
                    junit '**/build/test-results/test/*.xml' //make the junit test results available in any case (success & failure)
                }
			}
		}

		stage('Static code analysis') {
			steps {
				try {
                        sh './gradlew checkstyleMain --no-daemon' //run a gradle task
                } finally {
                    checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'build/reports/checkstyle/main.xml', unHealthy: ''
                }
			}
		}
	}
}
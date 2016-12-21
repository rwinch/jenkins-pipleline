stage('Build') {
	parallel test: {
		stage('Test') {
			node {
				checkout scm
				try {
					sh './gradlew clean test'
				} finally {
					junit '**/build/*-results/*/*.xml'
				}
			}
		}
	},

	itest: {
		stage('iTest') {
			node {
				checkout scm
				sh './gradlew iTest'
			}
		}
	},

	stageDocs: {
		stage('stage docs') {
			node {
				checkout scm
				sh './gradlew stageDocs'
			}
		}
	}
}

stage('Deploy') {
	if (currentBuild.result == 'SUCCESS') {
		sh './gradlew deploy'
	}
}
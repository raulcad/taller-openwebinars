pipeline {
	agent any
	stages {
		stage('Obtener el repositorio') {
			steps {
				git branch: 'main', url: 'https://github.com/raulcad/taller-openwebinars.git'
			}
		}
		stage('Generar la documentación') {
			steps {
				sh "doxygen"
			}
		}
	}
	post {
		publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'html/', reportFiles: 'files.html', reportName: 'Documentación', reportTitles: ''])
	}
}

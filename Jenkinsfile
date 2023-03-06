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
				sh "zip documentation.zip -r html/*"
			}
		}
		stage('Tests unitrios') {
			steps {
				sh 'make tests-xml'
				junit 'reports/cmocka/*.xml'
			}
		}
		stage('Análisis estático') {
			steps {
				sh 'make cppcheck-xml'
				//recordIssues(tools: [cppCheck(pattern: 'reports/cppcheck/*.xml')])
				recordIssues qualityGates: [[threshold: 1, type: 'TOTAL', unstable: false]], tools: [cppCheck(pattern: 'reports/cppcheck/*.xml')]
			}
		}
	}
	post {
		success {
//			publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'html/', reportFiles: 'files.html', reportName: 'Documentación', reportTitles: ''])
                	archive 'documentation.zip'
		}
	}
}

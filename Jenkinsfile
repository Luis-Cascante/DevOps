pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install') {
            steps {
                bat 'npm install'
            }
        }

        stage('Test') {
            steps {
                // Creamos el directorio si no existe
                bat 'if not exist test-results mkdir test-results'
                
                // Ejecutamos tu script de CI definido en package.json
                bat 'npm run test:ci'
            }
            post {
                always {
                    // Publicar resultados (JUnit viene por defecto con Jenkins)
                    junit 'test-results/**/*.xml'
                }
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'coverage/**', allowEmptyArchive: true
            }
        }
    }
}
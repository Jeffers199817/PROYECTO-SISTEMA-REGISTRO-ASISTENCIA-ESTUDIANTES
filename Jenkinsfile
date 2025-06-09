// Jenkinsfile - Versión 2 (más robusta)
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Simulando la compilación del proyecto...'
                // Aquí van tus comandos de compilación
                // sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Simulando la ejecución de pruebas...'
                // Aquí van tus comandos de prueba
                // sh 'npm test'
            }
        }
    }

    // El bloque 'post' se ejecuta DESPUÉS de todas las stages.
    // Aquí es donde reportaremos el estado a GitHub.
    post {
        always {
            script {
                // Definimos el nombre del status check.
                // DEBE SER EL MISMO que pongas en la regla de protección de rama.
                def contextName = "continuous-integration/jenkins"

                // Verificamos el resultado del build actual y reportamos.
                if (currentBuild.currentResult == 'SUCCESS') {
                    echo "Build exitoso. Reportando 'SUCCESS' a GitHub."
                    updateGitCommitStatus(
                        state: 'SUCCESS',
                        context: contextName,
                        message: 'El build ha finalizado con éxito.'
                    )
                } else if (currentBuild.currentResult == 'UNSTABLE') {
                    echo "Build inestable. Reportando 'FAILURE' a GitHub."
                    updateGitCommitStatus(
                        state: 'FAILURE',
                        context: contextName,
                        message: 'El build es inestable (ej: tests con fallos).'
                    )
                } else { // FAILURE, ABORTED, etc.
                    echo "Build fallido. Reportando 'FAILURE' a GitHub."
                    updateGitCommitStatus(
                        state: 'FAILURE',
                        context: contextName,
                        message: 'El build ha fallado.'
                    )
                }
            }
        }
    }
}

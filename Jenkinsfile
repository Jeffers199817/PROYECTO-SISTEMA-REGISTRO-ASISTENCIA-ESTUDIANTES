// Jenkinsfile - Versión 3 (Final para Job de tipo "Pipeline")
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Simulando la compilación del proyecto...'
                // Aquí van tus comandos de compilación
            }
        }
        stage('Test') {
            steps {
                echo 'Simulando la ejecución de pruebas...'
                // Aquí van tus comandos de prueba
            }
        }
    }

    post {
        always {
            script {
                // Definimos el nombre del status check.
                def contextName = "continuous-integration/jenkins"

                // Usamos la variable 'currentBuild.currentResult' para determinar el estado.
                // SUCCESS, UNSTABLE, FAILURE, etc.
                def buildResult = currentBuild.currentResult
                
                // Mapeamos el resultado de Jenkins a un estado que GitHub entienda.
                // GitHub usa: success, failure, error, pending.
                def githubState = 'pending' // Estado por defecto
                def githubMessage = ''

                if (buildResult == 'SUCCESS') {
                    githubState = 'success'
                    githubMessage = '¡El build ha finalizado con éxito!'
                } else if (buildResult == 'UNSTABLE') {
                    githubState = 'failure' // Unstable se considera un fallo para el PR
                    githubMessage = 'El build es inestable (ej: tests con fallos).'
                } else { // FAILURE, ABORTED
                    githubState = 'failure'
                    githubMessage = 'El build ha fallado.'
                }

                echo "Build finalizado con resultado: ${buildResult}. Reportando '${githubState}' a GitHub."

                // ¡ESTA ES LA LÍNEA CORREGIDA!
                // Usamos el método que sí está disponible en este contexto.
                setGitHubPullRequestStatus(
                    status: githubState,
                    context: contextName,
                    message: githubMessage
                )
            }
        }
    }
}

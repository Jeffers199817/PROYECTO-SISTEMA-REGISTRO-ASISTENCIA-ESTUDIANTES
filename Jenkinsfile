// Jenkinsfile - Versión 4 (Corrección Final)
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
                def contextName = "continuous-integration/jenkins"
                def buildResult = currentBuild.currentResult
                def githubState = 'pending'
                def githubMessage = ''

                if (buildResult == 'SUCCESS') {
                    githubState = 'success'
                    githubMessage = '¡El build ha finalizado con éxito!'
                } else if (buildResult == 'UNSTABLE') {
                    githubState = 'failure'
                    githubMessage = 'El build es inestable (ej: tests con fallos).'
                } else {
                    githubState = 'failure'
                    githubMessage = 'El build ha fallado.'
                }

                echo "Build finalizado con resultado: ${buildResult}. Reportando '${githubState}' a GitHub."

                // =======================================================
                // ¡AQUÍ ESTÁ LA CORRECCIÓN! Cambiamos 'status' por 'state'
                // =======================================================
                setGitHubPullRequestStatus(
                    state: githubState,  // <-- ESTA ES LA LÍNEA CORREGIDA
                    context: contextName,
                    message: githubMessage
                )
            }
        }
    }
}

// Jenkinsfile - Versión Final Definitiva
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
                
                // =======================================================
                // ¡LA CORRECCIÓN CRÍTICA ESTÁ AQUÍ!
                // Los estados deben estar en MAYÚSCULAS.
                // =======================================================
                def githubState
                def githubMessage

                if (buildResult == 'SUCCESS') {
                    githubState = 'SUCCESS' // <-- ANTES: 'success'
                    githubMessage = '¡El build ha finalizado con éxito!'
                } else { // UNSTABLE, FAILURE, ABORTED
                    githubState = 'FAILURE' // <-- ANTES: 'failure'
                    githubMessage = 'El build ha fallado o es inestable.'
                }

                echo "Build finalizado con resultado: ${buildResult}. Reportando '${githubState}' a GitHub."

                setGitHubPullRequestStatus(
                    state: githubState,
                    context: contextName,
                    message: githubMessage
                )
            }
        }
    }
}

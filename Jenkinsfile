// Jenkinsfile
pipeline {
    agent any // Ejecutar en cualquier agente disponible

    // Esta opción es CLAVE. Define el nombre del status check que verás en GitHub.
    options {
        buildStatus(context: "continuous-integration/jenkins") 
    }

    stages {
        stage('Build') {
            steps {
                echo 'Simulando la compilación del proyecto...'
                // REEMPLAZA ESTO con tu comando real. Ejemplos:
                // sh 'mvn clean install'   // Para proyectos Java con Maven
                // sh 'npm install'         // Para proyectos Node.js
            }
        }
        stage('Test') {
            steps {
                echo 'Simulando la ejecución de pruebas...'
                // REEMPLAZA ESTO con tu comando de pruebas. Ejemplos:
                // sh 'mvn test'
                // sh 'npm test'
            }
        }
    }
    
    post {
        // Jenkins reporta el estado automáticamente gracias al plugin,
        // pero esto es útil para ver mensajes en la consola de Jenkins.
        success {
            echo "¡Todo salió bien! El status check en GitHub será 'success'."
        }
        failure {
            echo "¡Algo falló! El status check en GitHub será 'failure'."
        }
    }
}

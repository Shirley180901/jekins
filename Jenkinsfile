pipeline {
    agent any

    tools {
        nodejs "Node25" // Configura una instalación de Node.js en Jenkins
        dockerTool 'Dockertool'  // Cambia el nombre de la herramienta según tu configuración en Jenkins
    }

    stages {
        stage('Construir Imagen Docker') {
            steps {
                // Mantiene la red host para que no se congele
                sh 'docker build --network=host -t hola-mundo-node:latest .'
            }
        }

        stage('Ejecutar Contenedor Node.js') {
            steps {
                sh '''
                    # Detener y eliminar cualquier contenedor previo con este nombre
                    docker stop hola-mundo-node || true
                    docker rm hola-mundo-node || true

                    # Se cambia el puerto externo a 3050 para evitar el error "port is already allocated"
                    docker run -d --name hola-mundo-node -p 3050:3000 hola-mundo-node:latest
                '''
            }
        }
    }
}

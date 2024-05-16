pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    // Clonar el repositorio
                    //git 'https://github.com/rduserjob/pipeline/nginx'
                    // Construir la imagen Docker
                    sh 'ls -l && pwd'
                    sh 'docker build -t ngninx .'
                }
            }
        }
        stage('Run Container') {
            steps {
                script {
                    // Levantar el contenedor
                    sh 'docker run -d --name my-app-container nginx'
                }
            }
        }
        stage('Push Image to DockerHub') {
            steps {
                script {
                    // Iniciar sesión en DockerHub
                    sh 'docker login -u tu_usuario_dockerhub -p tu_contraseña_dockerhub'
                    // Etiquetar la imagen
                    sh 'docker tag my-app tu_usuario_dockerhub/my-app'
                    // Subir la imagen a DockerHub
                    sh ' docker push tu_usuario_dockerhub/my-app'
                }
            }
        }
    }
}

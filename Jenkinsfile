pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                script {
                    // Clonar el repositorio
                    // sh 'git clone https://github.com/rduserjob/pipeline.git'
                    //Instalamos Hadolint para chequear la imagen
                    sh 'docker pull hadolint/hadolint'
                    // Construir la imagen Docker
                    sh 'ls -l && pwd'
                    sh 'docker build -f /var/lib/jenkins/workspace/test/nginx -t nginx .'
                    //Chequear la imagen creada
                    sh 'docker images'
                    // Chequear con Hadolint
                    sh 'docker run --rm -i hadolint/hadolint < /var/lib/jenkins/workspace/test/nginx' 
                }
            }
        }
        stage('Run Container') {
            steps {
                script {
                    // Levantar el contenedor
                    sh 'docker run -d --name my-app-container nginx'
                    //chequear que el contenedor este corriendo
                    sh'docker  ps'
                    // Para Testear el correcto funcionamiento
                    sh'curl localhost:8083'
                }
            }
        }
        stage('Push Image to DockerHub') {
            steps {
                script {
                    // Iniciar sesión en DockerHub
                    sh 'docker login -u oahp -p caramelos1'
                    // Etiquetar la imagen
                    sh 'docker tag nginx oahp/nginxosmar'
                    // Subir la imagen a DockerHub
                    sh ' docker push tu_usuario_dockerhub/nginxosmar'
                }
            }
        }
    }
}

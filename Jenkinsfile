pipeline {
    agent any
    stages {
        stage('Preparar subdirectorio del sonar-scanner') {
            agent { node { label 'penpen' } } // Especifica el nodo penpen para este stage
            steps {
                script {
                    // Cambia el nombre del subdirectorio a sonar-scanner
                    dir('sonar-scanner') {
                        // Clonar el repositorio externo dentro del subdirectorio sonar-scanner
                        git 'https://github.com/JFEspanolito/PlantillaFlujos2025UiPath.git'
                    }
                }
            }
        }
        stage('Usar Jenkinsfile del sonar-scanner') {
            agent { node { label 'penpen' } } // Especifica el nodo penpen para este stage 
            steps {
                script {
                    dir('sonar-scanner') {
                        // Cargar el Jenkinsfile externo
                        load 'Jenkinsfile.groovy'
                    }
                }
            }
        }
    }
}
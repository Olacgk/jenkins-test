pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK'
    }

    environment {
        SONAR_SCANNER_HOME = tool 'SonarQubeScanner'
        SONAR_TOKEN = credentials('sonar-token')
    }

    stages {

        // Étape 1 : Vérification de l'environnement
        stage('Vérification Environnement') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'mvn --version'
                        sh 'java --version'
                    } else {
                        bat 'mvn --version'
                        bat 'java --version'
                    }
                }
            }
        }

        // Étape 2 : Analyse SonarQube
        stage('Analyse SonarQube') {
            steps {
                script {
                    if (isUnix()) {
                        sh "${SonarQube}/bin/sonar-scanner -Dsonar.projectKey=jenkins -Dsonar.host.url=http://localhost:9000 -Dsonar.login=${SonarQube_token}"
                    } else {
                        bat "${SonarQube}\\bin\\sonar-scanner.bat -Dsonar.projectKey=my-project -Dsonar.host.url=http://localhost:9000 -Dsonar.login=${SonarQube_token}"
                    }
                }
            }
        }

    }

    
}
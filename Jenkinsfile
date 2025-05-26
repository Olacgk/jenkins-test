pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK'
    }

    environment {
        SONAR_SCANNER_HOME = tool 'SonarQubeScanner'
        SONAR_TOKEN = credentials('SonarQube_token')
    }

    stages {

        // Étape 1 : Vérification de l'environnement
        // stage('Vérification Environnement') {
        //     steps {
        //         script {
        //             if (isUnix()) {
        //                 sh 'mvn --version'
        //                 sh 'java --version'
        //             } else {
        //                 bat 'mvn --version'
        //                 bat 'java --version'
        //             }
        //         }
        //     }
        // }

        // Étape 2 : Analyse SonarQube
        stage('Analyse SonarQube') {
            steps {
                script {
                    if (isUnix()) {
                        sh "${SONAR_SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=jenkins -Dsonar.host.url=http://localhost:9000 -Dsonar.login=${SONAR_TOKEN}"
                    } else {
                        bat "${SONAR_SCANNER_HOME}\\bin\\sonar-scanner.bat -Dsonar.projectKey=jenkins -Dsonar.host.url=http://localhost:9000 -Dsonar.login=${SONAR_TOKEN}"
                    }
                }
            }
        }

    }

    
}
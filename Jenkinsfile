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
         stages {
            stage('SonarQube Analysis') {
                steps {
                    withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                        bat """
                            sonar-scanner \
                            -Dsonar.projectKey=jenkins \
                            -Dsonar.host.url=http://localhost:9000 \
                            -Dsonar.login=%SONAR_TOKEN%
                        """
                    }
                }
            }
        }

    }

    
}
pipeline {
    agent any
    options { skipDefaultCheckout(true) }
    environment {
        JAVA_HOME = '/usr/lib/jvm/java-21-openjdk-amd64'
        PATH = "/opt/aminedevops-tools/maven/bin:${env.PATH}"
    }
    stages {
        stage('Recuperation depuis GitHub') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-projet-spring',
                    url: 'git@github.com:AmineBenAmara/DevOps-AppGestionDesProjets.git'
            }
        }
        stage('Generation du livrable JAR') {
            steps {
                dir('backend') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }
    }
    post {
        success {
            archiveArtifacts artifacts: 'backend/target/*.jar', fingerprint: true
        }
    }
}

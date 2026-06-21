pipeline {
    agent {
        docker {
            image 'maven:3.9.6-eclipse-temurin-21-alpine'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                git(
                    url: 'git@github.com:Sumanta84/simple-java-maven-app.git',
                    branch: 'main',
                    credentialsId: 'simple-java-maven-app'
                )
            }
        }

        stage('Build') {
            steps {
                sh '''
                    mkdir -p /tmp/m2repo
                    mvn -Dmaven.repo.local=/tmp/m2repo clean package
                '''
            }
        }
    }
}
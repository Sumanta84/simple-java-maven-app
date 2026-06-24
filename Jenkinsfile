pipeline {
    agent {
        docker {
            image 'maven:3.9.16-eclipse-temurin-21-alpine'
            args '-v /var/jenkins_home/.m2:/var/jenkins_home/workspace/1.first-job-Java sample-project/.m2'
        }
    }

    environment {
        APP_NAME = 'sample-app'
        MAVEN_OPTS='-Dmaven.repo.local=/var/jenkins_home/workspace/1.first-job-Java sample-project/.m2/repository'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'git@github.com:Sumanta84/simple-java-maven-app.git',
                    credentialsId: 'simple-java-maven-app'
            }
        }

        stage('Debug') {
            steps {
                sh '''
                    pwd
                    ls -ltr /var/jenkins_home
                    ls -ltr /var/jenkins_home/workspace/1.first-job-Java sample-project/.m2
                '''
            }
        }
        stage('Build') {
            steps {
                sh '''
                    mvn -Dmaven.repo.local=/var/jenkins_home/workspace/1.first-job-Java sample-project/.m2/repository clean package                   
                    ls /var/jenkins_home/workspace/1.first-job-Java sample-project/.m2
                '''
            }
        }
        stage('Test') {
            steps {
                sh 'mvn -Dmaven.repo.local=/var/jenkins_home/workspace/1.first-job-Java sample-project/.m2 test'
            }
        }
    }

    post {
        success {
            echo "${env.APP_NAME} pipeline completed successfully"
        }
        failure {
            echo "${env.APP_NAME} pipeline failed. Check logs"
        }
    }
}
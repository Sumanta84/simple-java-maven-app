pipeline{
    agent{
        docker{
            image 'maven:3.9.16-eclipse-temurin-21-alpine'
            args '-v /var/jenkins_home:/var/jenkins_home'
        }
    }
    environment{
        APP_NAME='sample-app'
        //MAVEN_OPTS='-Dmaven.repo.local=/var/jenkins_home/.m2/repository'
    }
    stages{
        stage('Checkout'){
            steps{
                 git 
                    branch: 'main',
                    url: 'git@github.com:Sumanta84/simple-java-maven-app.git',
                    credentialsId: 'simple-java-maven-app'
            }
        }
        stage('Debug'){
            steps{
                sh '''
                    pwd
                    ls -ltr /var/jenkins_home
                    ls -ltr /var/jenkins_home/.m2
                '''
            }
        }
        stage('Build'){
            steps{
                sh '''
                    mvn -Dmaven.repo.local=.m2/repository clean package

                '''
            }
        }
        stage('Test'){
            steps{
                sh 'mvn -Dmaven.repo.local=.m2/repository test'
            }
        }
    }
    post{
        success{
            echo "${env.APP_NAME} pipeline completed successfully"
        }
        failure{
            echo "${env.APP_NAME} pipeline failed. Check logs"
        }
    }
}
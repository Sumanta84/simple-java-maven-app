pipeline{
    agent{
        docker{
            image 'maven:3.9.16-eclipse-temurin-21-alpine'
            args '-v /var/jenkins_home/.m2:/root/.m2'
        }
    }
    environment{
        APP_NAME = 'sample-app'
    }
    stages{

        stage('Checkout'){
            steps{
                git(
                    url:'git@github.com:Sumanta84/simple-java-maven-app.git',
                    branch:'main',
                    credentialsId:'simple-java-maven-app'
                )
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Test'){
            steps{
                sh 'mvn test'
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

pipeline{
    agent{
        docker{
            image 'maven:3.9.16-eclipse-temurin-21-alpine'
            args '-v $HOME/.m2:/root/.m2'
        }
    }
    environment{
        APP_NAME='sample-app'
    }
    stages{
        stage('Checkout'){
            steps{
                git( url:'git@github.com:Sumanta84/simple-java-maven-app.git',
                    branch:'master',
                    credentialsId:'simple-java-maven-app'
                )
            }
        }
        // stage('Debug'){
        //     steps{
        //         sh '''
        //             cat /etc/passwd
        //             cat /etc/group
        //             echo $HOME
        //             ls -ld /root
        //             ls -ld /root/.m2
        //         '''
            // }
       // }
        stage('Build'){
            steps{
                sh 'mvn clean package'
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

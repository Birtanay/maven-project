pipeline {
    agent any

    stages{
        stage('Build'){
            steps {
                sh 'C:\\maven\\apache-maven-3.6.0\\bin\\mvn clean package'
                sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"
            }
            

        }
    }
}
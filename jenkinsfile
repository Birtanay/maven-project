pipeline {
    agent any

    stages{
        stage('Build'){
            steps {
                bat 'C:\\maven\\apache-maven-3.6.0\\bin\\mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deploy To Staging') {
            steps {
                build job: 'Tomcat8-DeployTo-Staging'
            }
        }

        stage ('Deploy To Production') {

            steps {
                timeout(time:5, unit:'DAYS'){
                    input message:'Are you approving PRODUCTION Deployment?'
                }

                build job: 'tomcat8-deployto-prod'
            }

            post {
                success {
                    echo 'Code Deployed To PRODUCTION !!!'
                }

                failure {
                    echo 'Deployment To Production FAILED!!!'
                }
            }
        }
    }
}
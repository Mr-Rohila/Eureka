pipeline {
    agent any
    
    environment {
        MAVEN_HOME = tool 'Maven'
    }

    stages {
        stage('Build') {
            steps {
                bat "\"${MAVEN_HOME}\\bin\\mvn\" clean package"
            }
        }

        stage('Stop Service') {
            steps {
                bat "net stop Eureka"
                sleep time: 10, unit: 'SECONDS'
             	bat 'sc query Eureka | find "STATE" | find "STOPPED" && echo "Service stopped"'  
            }
        }

 		stage('Copy Jar File') {
            steps {
                bat "copy /Y target\\Eureka.jar G:\\HRMS_API\\Eureka"
            }
        }
    }
    post {
        always {
           bat "nssm start Eureka"
        }
    }
}
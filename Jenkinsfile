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
                bat "nssm stop Eureka"
            }
        }

 		stage('Copy Jar File') {
            steps {
                bat "copy /Y target\\Eureka.jar G:\\HRMS_API\\Eureka"
            }
        }

        stage('Run Service') {
            steps {            
                bat "nssm start Eureka"
            }
        }
    }
}
pipeline{
    agent any
    environment{
        TOMCAT_URL = "http://3.88.2.185:8080/"
        TOMCAT_USERNAME = "admin"
        TOMCAT_PASSWORD = "admin"
        WAR_FILE = "**.*war"
        CONTEXT_PATH = "/opt/tomcat/webapps/**.*war"
    }
    stages {
        stage('checkout SCM') {
            steps {
                git branch: 'master',
                        credentialsId: '54d66e02-c222-4d57-811f-f92654e7b84e',
                        url: 'https://github.com/suraj251994/maven-project.git'
                        echo 'Git Checkout Completed'
            }
        }
        stage('Build'){
        steps{
            sh """
            mvn clean install
            """
        }
      }
	     stage('Deploy'){
        steps{
		     sshagent(['3.88.2.185']) {
             sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ubuntu@3.88.2.185:/opt/tomcat/webapps"
            } 
        }
      }
    }
}

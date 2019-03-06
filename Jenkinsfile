pipeline {
    agent any
    tools {
        maven 'localMaven'
    }

    triggers {
         pollSCM('* * * * *')
     }

    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
                sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"
                sh "docker run -it --name tomcat-${env.BUILD_ID} -p 8181:8080 tomcatwebapp:${env.BUILD_ID} bash"
            }
        }
    }
}
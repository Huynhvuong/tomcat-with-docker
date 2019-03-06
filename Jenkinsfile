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
                sh "docker build /var/lib/jenkins/workspace/Tomcat-with-Docker/Dockerfile -t tomcatwebapp:${env.BUILD_ID}"
                sh "docker run -d  -p 8181:8080 --name tomcat-${env.BUILD_ID} tomcatwebapp:${env.BUILD_ID}"
            }
        }
    }
}
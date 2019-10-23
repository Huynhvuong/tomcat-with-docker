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
                sh 'cd /var/lib/jenkins/workspace/Tomcat-with-Docker/'
                sh 'mvn clean package'
                sh "docker build /var/lib/jenkins/workspace/Tomcat-with-Docker/ -t tomcatwebapp:${env.BUILD_ID}"
                //sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"
                sh "docker run -d  -p 8181:8080 --name tomcat-${env.BUILD_ID} tomcatwebapp:${env.BUILD_ID}"
            }
        }
    }
}

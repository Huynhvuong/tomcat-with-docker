pipeline {
    agent any
    tools {
        maven 'localMaven'
        docker 'LocalDocker'
    }
    

    triggers {
         pollSCM('* * * * *')
     }

    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
                //sh "docker build /var/lib/jenkins/workspace/Tomcat-with-Docker/ -t tomcatwebapp:${env.BUILD_ID}"
                //sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"
                sh "/Applications/Docker.app/Contents/Resources/bin/docker build . -t tomcatwebapp:${env.BUILD_ID} "
                sh "/Applications/Docker.app/Contents/Resources/bin/docker run -d  -p 8181:8080 --name tomcat-${env.BUILD_ID} tomcatwebapp:${env.BUILD_ID}"
            }
        }
    }
}

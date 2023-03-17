pipeline {
  agent none
  parameters { string(name: 'jfrog_user', defaultValue: '', description: ' this is user name for jfrog') 
               string(name: 'jfrog_pass', defaultValue: '', description: ' this is password for jfrog') }
  environment {
                MVN_HOME = "/tmp/maven3.9/"
                     
            }
  
  stages {
    
    stage('build code and push code to artifact repo ') {
      agent { label 'jenkin-azure' }
      steps {
        sh "export PATH=$PATH:${env.MVN_HOME}/bin && mvn clean deploy"
      }
    }
    
    stage('deployment on tomcat') {
      agent { label 'jenkin-azure' }
      steps {
        sh """
             wget --http-user=${jfrog_user}  --http-password=${jfrog_pass} https://devops400.jfrog.io/artifactory/devops/com/mycompany/app/my-app-jp/2.0-SNAPSHOT/my-app-jp-2.0-20230316.063100-1.war
             cp my-app-jp-2.0-20230316.063100-1.war /home/rocky/tomcat9/webapps/
          """
      }
    }
  }
  }

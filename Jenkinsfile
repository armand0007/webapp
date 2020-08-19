  pipeline {
    agent any
    tools {
      maven 'Maven'
    }
    stages {
     stage ('Initialize') {
       steps  {
          sh '''
                 echo "PATH = ${PATH}"
                 echo  "M2_HOME = ${M2_HOME}"
             '''
     }
   }

   stage ('check-Git-Secrets'){
     steps {
       sh 'rm truflehog || true'
       sh 'docker run gesellix/trufflehog https://github.com/armand0007/webapp.git > truflehog'
       sh 'cat truflehog'
     }
   }

   stage {'Source Composition Analysis'} {
     steps { 
       sh 'rm owasp* || true'
       sh 'wget "https://raw.githubusercontent.com/armand0007/webapp/master/owasp-dependency-check.sh"'
       sh 'chmod +x owasp-dependency-check.sh'
       sh 'bash owasp-dependency-check.sh'

     }
   }
 
   stage ('Build') {
     steps {
     sh 'mvn clean package'
      }
    }  

   stage ('Deploy-To-Tomcat') {
           steps {
          sshagent (['tomcat']) {
               sh 'scp -o StrictHostkeyChecking=no target/*.war ubuntu@54.144.145.92:/prod/apache-tomcat-8.5.57/webapps/webapp.war'
             }
          }
  
   }

 }
}   
 

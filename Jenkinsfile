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
 
 stage ('Build') {
   steps {
   sh 'mvn clean package'
  }
  }
 stage ('Deploy-To-Tomcat') {
      step {
        sshagent (['tomcat']) {
          sh 'scp -o StrictHostkeyChecking=no target/*.war ubuntu@54.144.145.92:/prod/apache-tomcat-8.5.57/webapps/webapp.war'
}
}

    }
  }
}

pipeline {
  agent any
  tools {
    maven 'Maven'
  }
  stages {
   stages ( 'Initialize') {
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
  
}
}

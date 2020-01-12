pipeline {
   agent any

   stages {
      stage('Build') {
         steps {
            echo 'Hello World';
            echo 'Hi this is build stage'
            build 'freestyle-project'
         }
      }
      stage('Test') {
         steps {
            echo 'Hi this is test stage. Running some test cases'
         }
      }
   }
}

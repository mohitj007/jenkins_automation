pipeline {
   agent any

   stages {
      stage('Creating base jobs') {
          steps {
		         echo "Building pipeline for base jobs creation"
             build 'pipeline'
          }
      }
      stage('Checking out code') {
         steps {
            echo 'Checking out clean code'
            build 'test'
         }
      }
      stage('Deploying docker compose') {
         steps {
            echo 'Deploying docker compose file'
            build job: 'test1', propagate: false
         }
      }
      stage('Cleaning repository') {
         steps {
            echo 'cleaning git repository'
            build 'test2'
         }
      }
   }
}

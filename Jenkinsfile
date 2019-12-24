pipeline {
   agent any

   stages {
      stage('Checking out code') {
          steps {
             echo "Checking out jobs code from github"
	     git 'https://github.com/mohitj007/jenkins_automation.git'
             sh label: '', script: '''cd /tmp/; if [ -f /tmp/jenkins-cli.jar ]; then echo \\\'Jenkins cli already present\\\'; else wget http://localhost:8080/jnlpJars/jenkins-cli.jar; fi;
             cliconnect="java -jar /tmp/jenkins-cli.jar -s http://`hostname -i`:8080 -auth admin:admin"
             cd /tmp/test2; for i in `ls -l|awk \'{print $9}\'`; do file=`echo $i|cut -d \'.\' -f1`; echo $file; $cliconnect create-job $file < `pwd`/$i; done
             $cliconnect reload-configuration'''
          }
      }
      stage('Checking out codespaces repo') {
         steps {
            echo 'Checking out clean code'
            build 'job1'
         }
      }
      stage('Deploying docker compose') {
         steps {
            echo 'Deploying docker compose file'
            build job: 'job2', propagate: false
         }
      }
      stage('Cleaning repository') {
         steps {
            echo 'cleaning git repository'
            build 'job3'
         }
      }
   }
}

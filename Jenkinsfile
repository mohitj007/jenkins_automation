pipeline {
   agent any

   stages {
      stage('Creating base jobs') {
          steps {
             sh label: '', script: '''cd /tmp/; if [ -f /tmp/jenkins-cli.jar ]; then echo \'Jenkins cli already present\'; else wget http://localhost:8080/jnlpJars/jenkins-cli.jar; fi;
             cliconnect="java -jar /tmp/jenkins-cli.jar -s http://`hostname -i`:8080 -auth admin:admin"
             cd $WORKSPACE; pwd; for i in `cat jobstobuild`; do set +e; $cliconnect list-jobs|grep -i $i; if [ $? == 0 ]; then echo "Job $i already present"; else "Job $i is absent"; $cliconnect create-job $i < `pwd`/$i.xml; sleep 2; set -e; fi; done
             $cliconnect reload-configuration'''
             echo "Building base jobs pipeline"
          }
      }
      stage('Checking out code') {
         steps {
            echo 'Building job 1'
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

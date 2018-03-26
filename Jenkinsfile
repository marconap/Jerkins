pipeline {
    agent any 
     environment{
        CMD = "curl -u admin:adminadmin -X GET 'http://172.18.2.25:80/jk-manager?cmd=update&from=list&w=balancer&sw=node1&vwa=1'"
                }
   
    stages {
        stage('Stage 1') {
            steps {
                echo 'Prova SCM!' 
            }
        }
        stage('Stage 2') {
            steps {
                sh "${CMD}"
                   }
        }
        stage('wait_1_min') {
            steps {
                def time = "${time}"
            echo "Waiting ${SLEEP_TIME_IN_SECONDS} seconds for deployment to complete prior to deploy"
            sleep time.toInteger() // seconds
                    }    
                 }
        }
    }


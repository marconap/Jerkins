pipeline {
    agent any 
     environment{
        CMD_balancer = "curl -u admin:adminadmin -X GET 'http://172.18.2.25:80/jk-manager?cmd=update&from=list&w=balancer&sw=node1&vwa=1'"
        CMD_deploy_T1 = "curl -u admin:adminadmin -X GET 'http://172.18.2.26:8080/manager/text/deploy?path=/test##2'"
                }
   stages {
                stage('Stage 1') {
                                steps {
                                        echo 'Prova SCM!' 
                                      }
                                 }
                
                stage('Stage 2') {
                                steps {
                                        sh "${CMD_balancer}"
                                      }
                                 }
       
                stage('wait_1_min') {
        
                               steps {
                                     script{
                                             def time = params.time
                                             echo "Waiting time seconds for deployment to complete prior to deploy"
                                             sleep time.toInteger() // seconds
                                            }
                                    }    
                                    }
        }
  
    post { 
        always { 
            sh "${CMD_deploy_T1}"
        }
    }
    }


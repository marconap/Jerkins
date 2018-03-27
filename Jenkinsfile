pipeline {
    agent any 
     environment{
         CMD_balancer_disable = "curl -u ${userpass} -X GET 'http://${IP_httpd}/jk-manager?cmd=update&from=list&w=balancer&sw=node1&vwa=1'"
         CMD_balancer_enable  = "curl -u ${userpass} -X GET 'http://${IP_httpd}/jk-manager?cmd=update&from=list&w=balancer&sw=node1&vwa=0'"
         CMD_upload_app = "ssh - T ${IP_Tomcat1} && cd ${repository_path} && git pull origin master && cp -p *.war ${webapps_path}"       
        
                }
   stages {
                stage('Stage 1') {
                                steps {
                                        echo 'Prova SCM!' 
                                      }
                                 }
                
                stage('Stage 2') {
                                steps {
                                        sh "${CMD_balancer_disable}"
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
            
            sh "${CMD_upload_app}"
            sh "${CMD_balancer_enable}"
            
        }
    }
    }


pipeline {
    agent any 
     environment{
         CMD_balancer_node1_disable = "curl -u ${userpass} -X GET 'http://${IP_httpd}/jk-manager?cmd=update&from=list&w=balancer&sw=node1&vwa=1'"
         CMD_balancer_node1_enable  = "curl -u ${userpass} -X GET 'http://${IP_httpd}/jk-manager?cmd=update&from=list&w=balancer&sw=node1&vwa=0'"
         CMD_balancer_node2_disable = "curl -u ${userpass} -X GET 'http://${IP_httpd}/jk-manager?cmd=update&from=list&w=balancer&sw=node2&vwa=1'"
         CMD_balancer_node2_enable  = "curl -u ${userpass} -X GET 'http://${IP_httpd}/jk-manager?cmd=update&from=list&w=balancer&sw=node2&vwa=0'"
         CMD_upload_app = "ssh -T ${IP_Tomcat1} && cd ${repository_path} && git pull origin master && cp -p *.war ${webapps_path}"       
         CMD_deploy_app_T1 = "curl -u ${userpass} -X GET 'http://${IP_Tomcat1}/manager/text/deploy?war=file%3A%2Fusr%2Fshare%2Ftomcat%2Fwebapps%2Ftest%23%233&path=/test&version=3'"
         CMD_deploy_app_T2 = "curl -u ${userpass} -X GET 'http://${IP_Tomcat2}/manager/text/deploy?war=file%3A%2Fusr%2Fshare%2Ftomcat%2Fwebapps%2Ftest%23%233&path=/test&version=3'"
       
        }
   stages {
                stage('Deploy su Tomcat 1') {
                                steps {
                                         
                                         script {
                                             sh "${CMD_balancer_node1_disable}"
                                              sh "${CMD_deploy_app_T1}"
                                             input 'Continuare con il deploy?'
                                    
                                                }
                                    
                                      }
                                 }
                
                stage('Deploy su Tomcat 2') {
                                steps {
                                       sh "${CMD_balancer_node1_enable}"
                                       sh "${CMD_balancer_node2_disable}"
                                        sh "${CMD_deploy_app_T2}"
                                        input 'Terminare l\'aggiornamento?'

                                        
                                      }
                                 }
       
                stage('Termina aggiornamento') 
                            {
        
                               steps {
                                          sh "${CMD_balancer_node2_enable}"

                                    }    
                            }
        }
  
   
    }
    


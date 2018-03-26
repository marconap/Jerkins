pipeline {
    agent any 
    stages {
        stage('Stage 1') {
            steps {
                echo 'Prova SCM!' 
            }
        }
        stage('Stage 2') {
            steps {
                sh 'curl -X GET 172.18.2.25/jk-manager?cmd=update&from=list&w=balancer&sw=node1&vwa=1'
            }
        }
        stage('Stage 3') {
            steps {
                echo 'stage3!' 
            }
        }
    }
}

pipeline {
    agent any
    stages{
        stage ('serviceinstall'){
            steps{
                //sh "docker stop master"
                //sh "docker rm master"
                sh "rm -rf *"
                sh " yum install git -y"
                sh "yum install docker -y"
                sh "systemctl start docker"
            }
        }
        stage ('createconatainer'){
            steps{
                sh "docker run -itd -p 90:80 --name 22Q1 httpd"
            }
        }
        stage('deploy') { 
            agent{
                label{
                    label 'built-in'
                    customWorkspace "/mnt/psd"
                }
            }
            steps{
                sh "chmod -R 777 /mnt/psd/index.html "
                sh "docker cp /mnt/psd/index.html master:/usr/local/apache2/htdocs"
                
          }
        }
    }
}

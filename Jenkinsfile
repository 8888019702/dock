pipeline {
    agent any
    stages{
        stage ('serviceinstall'){
            steps{
                //sh "docker stop 22Q2"
                //sh "docker rm 22Q2"
                sh "rm -rf *"
                sh " yum install git -y"
                sh "yum install docker -y"
                sh "systemctl start docker"
            }
        }
        stage ('createconatainer'){
            steps{
                sh "docker run -itd -p 100:80 --name 22Q2 httpd"
            }
        }
        stage('deploy') { 
            agent{
                label{
                    label 'built-in'
                    customWorkspace "/mnt/shubzz"
                }
            }
            steps{
                sh "chmod -R 777 /mnt/shubzz/index.html "
                sh "docker cp /mnt/shubzz/index.html 22Q2:/usr/local/apache2/htdocs"
                
          }
        }
    }
}

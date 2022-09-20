pipeline{
    agent any 
       stages{
        stage('SCM'){
            steps{
                git 'https://github.com/siva-pra/jenkins-docker-k8s.git'
            }
        }
        stage("docker image build"){
             steps{
                    sh 'docker image build -t sivaprasad1996/app:latest .'
            }
        }
        stage('docker imgae push'){
             steps{
                 withCredentials([file(credentialsId: 'docker_passwd', variable: 'dockerpasswd')]){
                    sh 'docker login -u sivaprasad1996 -u ${dockerpasswd}' 
                    sh 'docekr image push sivaprasad1996/app:latest' 
                }
            }

        }
        stage('deploy app in k8s'){
          steps{
              kubernetsDeploy (configs: 'deploy-svc.yml', kubecifigId: 'k8sconfigfile')
          }  

        }   
    }
       
}
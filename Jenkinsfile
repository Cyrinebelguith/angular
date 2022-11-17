pipeline
{
  agent any 
  stages {
    stage('Pull') {
      steps{
	script{
	  checkout([$class: 'GitSCM' , branches: [[name: '*/master']],
	  userRemoteConfigs: [[ 
          url: 'https://github.com/Cyrinebelguith/angular.git']]])
	}
      }
    }	
    stage('build') {
     steps{
        script{
	  sh "npm ci"
	  sh "ansible-playbook ansible/build.yml  -i /ansible/inventory/host.yml -vvv" 
	}
      }
     }
    stage('create image & build docker') {
     steps {
        script{
          sh "ansible-playbook ansible/docker.yml -i ansible/inventory/host.yml"
         }
      }
    }
    stage('Push image to DOCKERHUB via ANSIBLE') {
     script {   
       sh 'ansible-playbook ansible/docker-registry.yml -i ansible/inventory/host.yml -vvv'
     }
   } 
    	
  }
}

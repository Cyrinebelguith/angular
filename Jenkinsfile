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

	  sh "ansible-playbook ansible/build.yml  -i /ansible/inventory/host.yml -e -vvv "

	}
      }
     }

	    	
  }
}

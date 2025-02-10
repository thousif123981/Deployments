pipeline {
 agent none
 parameters {
   string(name: 'ECRURL', defaultValue: '908027399517.dkr.ecr.ap-south-1.amazonaws.com', description: 'Please Enter ECR REGISTRY URL')
   string(name: 'IMAGE', defaultValue: 'demoappimage:24', description: 'Please Enter the Image to Deploy?')
   password(name: 'PASSWD', defaultValue: '', description: 'Please Enter your Gitlab password')
 }
 stages {
  stage('Deploy')
  {
    agent { label 'build' }
    steps { 
        git branch: 'main', credentialsId: 'GithubCred', url: 'https://github.com/thousif123981/Deployments.git'

	    sh "git config --global user.email "thousif.isaq1@gmail.com""
	    sh "git config --global user.name "thousif123981""
	    
	 	dir ("./k8smanifest") {
	      sh "sed -i 's/image:.*/image: $ECRURL$IMAGE/g' deployment.yaml" // make sure the ECRURL has \/ at the end
	    }
		sh 'git commit -a -m "New deployment for Build $IMAGE"'
		sh "git push https://thousif123981:$PASSWD@github.com/thousif123981/Deployments.git"
    }
  }
 }
}

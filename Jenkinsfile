properties([pipelineTriggers([githubPush()])])

pipeline {
    agent { 
      docker {
        image 'hashicorp/terraform:light'
        args  '--entrypoint='
      }
    }

    options {
       withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'ynov_16', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])	
    }

    environment {
     AWS_REGION = "eu-west-3"
}
    
    stages {
	stage('Init') {
	    steps {
		sh 'terraform init -backend-config=backend.tfvars'
	    }
        }
	stage('Plan') {
	    steps {
		sh 'terraform plan'
	    }
        }
	stage('Apply') {
	    steps {
		sh 'terraform apply -auto-approve'
	    }
	}
        stage('Output') {
            steps {
                sh 'terraform output'
            }
        }
   }
}

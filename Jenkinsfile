pipeline {
  agent {
    docker {
      image "bryandollery/terraform-packer-aws-alpine"
      args "-u root --entrypoint=''"
    }
  }
  environment {
    CREDS = credentials('bryan_aws_creds')
    AWS_ACCESS_KEY_ID = "${CREDS_USR}"
    AWS_SECRET_ACCESS_KEY = "${CREDS_PSW}"
    OWNER = 'renad'
    PROJECT_NAME = 'web-server'
  }
  stages {
    stage("build") {
      steps {
        sh 'packer build packer.json'
      }
    }
  }
  post {
    success {
        build quietPeriod: 0, wait: false, job: 'renad-jenkins-lab-2-tf'  
    }
  }
}

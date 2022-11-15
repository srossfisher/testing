pipeline {
  agent { label 'terraform'}
  options {
    skipDefaultCheckout(true)
  }
  stages{
    stage('clean workspace') {
      steps {
        cleanWs()
      }
    }
    stage('checkout terraform') {
      steps {
        checkout scm
      }
    }
    stage('checkout tfenv') {
      steps {
        script {          
          sh '''#!/bin/bash
          mkdir ./tfenv
          git clone https://github.com/tfutils/tfenv.git $(pwd)/.tfenv
          ''' 
        }
      }
    }
    stage('terraform install') {
      steps {
        script {
          
          sh '''#!/bin/bash
          chmod 755 ./tfinstall
          ./tfinstall apply -auto-approve -no-color
          '''
        
        }
      }
    }
    stage('terraform plan') {
      steps {
        script {
          
          sh '''#!/bin/bash
          CUSTOMBIN=$(pwd)/.tfenv/bin
          export PATH=$CUSTOMBIN:$PATH
          export TF_VAR_aws_access_key="AKIAZFD47TEBGLSFSDUQ"
          export TF_VAR_aws_secret_key="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"
          export TF_VAR_bucket_name="fnlsnfienednvkdnlsdncmrossf"
          export TF_VAR_region="eu-west-1"
          env
          terraform init
          terraform plan
          '''
          
        }       
      }
    }
    stage('terraform apply and destroy') {
      steps {
        script {
          
          sh '''#!/bin/bash          
          CUSTOMBIN=$(pwd)/.tfenv/bin
          export PATH=$CUSTOMBIN:$PATH
          export TF_VAR_aws_access_key="AKIAZFD47TEBGLSFSDUQ"
          export TF_VAR_aws_secret_key="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"
          export TF_VAR_bucket_name="fnlsnfienednvkdnlsdncmrossf"
          export TF_VAR_region="eu-west-1"
          terraform init
          #terraform apply -auto-approve
          #terraform destroy -auto-approve
          '''
          
        }
      }
    }    
  }
  post {
    always {
      cleanWs()
    }
  }
}



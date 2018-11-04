stage ('Checkout') {
    checkout scm
  }


def userInput =null
stage('input') {
    id: 'userInput', message: 'AWS Credentials?', parameters: [
        [$class: 'TextParameterDefinition',description: 'AWS Access Key ID', name: 'AWS_ACCESS_KEY_ID'],
        [$class: 'TextParameterDefinition',description: 'AWS Secret Key ID', name: 'AWS_SECRET_KEY_ID']
    ]

}


stage ('Terraform Plan') {
    sh './terraform plan -no-color -out=create.tfplan'
  }

 // Optional wait for approval
  


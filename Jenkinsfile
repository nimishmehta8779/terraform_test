#!/usr/bin/env groovy

import jenkins.model.jenkins


def inputaWSAccessKey
def inputAWSSecretKey

stage("Prompt user for Terraform variales") {
script  {

def userInput = input (
id: 'userInput', message 'Enter the terraform variables:?',
[
    parameters: [

string (defaultValue:'',
    description: 'Access key to AWS',
    name: 'AccessKey'),

string (defaultValue:'',
    description: 'Secret key to AWS',
    name: 'SeceretKey'),

    ] 
])

inputAccessKey = userInput.AccessKey?:''
inputAccessKey = userInput.AccessKey.trim()

inputSecretKey = userInput.SeceretKey?:''
inputSecretKey = userInput.SecretKey.trim()

}

}


node("linux") {

def basePath = './'
ansiColor ('xterm') {
stage ('Clean Workspace') {
step ([$class: 'WScleanup'])
    
}

stage('Pull Sourcecode') {
    checkout scm

}

stage('Prepare workspace') {

    def artifacts = ['terraform_0.11.10_linux_amd64.zip',
    'terraform.d/plugins/linux_amd64/terraform-provider-aws_v1.42.0_x4'
    ]

sh "chmod +x terraform-provide-*"

// unzip terraform zip file

sh "unzip terraform_0.11.10_linux_amd64.zip"

}

stage('Terraform plan') {

sh "./terraform init -plugin-dir =.${basepath}"
sh "./terraform plan -var aws_access_key=$inputAccessKey -var aws_secret_key=$inputSecretKey"

}

stage('Terraform apply') {
try {
sh "./terraform apply --auto-approve -var aws_access_key=$inputAccessKey -var aws_secret_key=$inputSecretKey"
}
catch (err)
{
    sh "./terraform destroy --auto-approve -var aws_access_key=$inputAccessKey -var aws_secret_key=$inputSecretKey"
    throw err
}

}

}


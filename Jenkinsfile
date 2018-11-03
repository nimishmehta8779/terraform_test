def userInput = true
def didTimeout = false


node {
    stage 'checkout'
       checkout scm

def tfHome = tool name: 'Terraform', type: 'com.cloudbees.jenkins.plugins.customtools.CustomTool'
env.PATH = "${tfHome}:${env.PATH}"

wrap([$class: 'AnsiColorBuildWrapper', colorMapName: 'xterm']) {
    stage 'init'

	if (fileExists(".terraform/terraform.tfstate")) {
                sh "rm -rf .terraform/terraform.tfstate"
            }
            if (fileExists("status")) {
                sh "rm status"
            }
       sh "./terraform --version"
       sh "./terraform init" 

 echo "Terraform Plan Exit Code: ${exitCode}"
   stage name: 'plan', concurrency: 1
        sh "./terraform plan --out plan"
    stage name: 'deploy'
       sh "./terraform apply plan"
}

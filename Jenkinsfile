node {
    stage 'checkout'
       checkout scm
    stage 'init'
       sh "./terraform init" 
   stage name: 'plan', concurrency: 1
        sh "./terraform plan --out plan"
    stage name: 'deploy'
       sh "./terraform apply plan"
}

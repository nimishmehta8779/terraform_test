node {
    stage 'checkout'
       checkout scm
    stage 'test'
       parallel (
            phase1: { sh "echo p1; sleep 20s; echo phase1" },
            phase2: { sh "echo p2; sleep 40s; echo phase2" }
        )
   stage name: 'plan', concurrency: 1
        sh "terraform plan --out plan"
    stage name: 'deploy'
       sh "terraform apply plan"
}

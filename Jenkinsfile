pipeline{
  agent {
    label 'SLAVE'
  }

  environment{
    TF_VAR_SSH = credentials('SSH_ROOT')
    TF_VAR_GIT = credentials('GitUserPass')
    TF_VAR_R   = credentials('RabbitMq')
  }

  stages{
    stage('Terramform init')
            {
              steps{
                sh '''
                  terraform get -update
                  terraform init
              '''
              }
            }
    stage('Terramform apply')
            {
              when{
                expression{
                  params.ACTION == 'APPLY'
                }
              }
              steps{
                sh '''
                  terraform apply -auto-approve
              '''
              }
            }
    stage('Terramform destroy')
            {
              when{
                expression{
                  params.ACTION == 'DESTROY'
                }
              }
              steps{
                sh '''
                  terraform destroy -auto-approve
              '''
              }
            }
  }
}
pipeline{
  agent any
  environment{
    APP_NAME = "git-argo-app"
   
  }
  stages{
        stage( 'Clear the Work Space'){
          steps{
            script{
              cleanWs()
            }
          }
        }
        stage('Checkout SCM'){
          steps{
            git branch: 'main', url: 'https://github.com/mukeshjava92/git_agrocd_CD.git'
            }
          }
       
            stage('Update deployment.yaml file'){
          steps{
            script{
            sh """
            cat deployment.yaml
            sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
            cat deployment.yaml
            """
            }
            }
            }
            stage('Push Deployment.yaml back to git'){
          steps{
            script{
            sh """
            git config --global user.name mukeshjava92
            git config --global user.mail mukeshjava92@gmail.com
            git add deployment.yaml
            git commit -m "Updated deployment.yaml file" 
            """
            withCredentials([string(credentialsId: 'gitcred', variable: 'gitcred')]) {
            sh 'git push "https://${gitcred}@github.com/mukeshjava92/git_agrocd_CD" main'
            }
            }
            }
            }
        }
   }

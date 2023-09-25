@Library('my-shared-library') _
pipeline {
    
    agent any
    parameters{

        choice(name:'action',choices:'create\ndelete',description:'choose create/destroy')
    }
    stages{
        when { expression { param.action == 'create'}}
        stage ("Git checkout"){
            steps{
                gitCheckout(
                    branch: "main",
                    url: "https://github.com/navedalisayyed/CICD-pipeline.git"
                )
                   

            }

        }
        stage ("MVN unit test"){
        when { expression { param.action == 'create'}}    
            steps{
               script{
                  mvnTest()
               }

            }

        }
        stage ("MVN integration test"){
        when { expression { param.action == 'create'}}    
            steps{
               script{
                  mvnIntegrationTest()
               }

            }
            
              
        }
    }
}

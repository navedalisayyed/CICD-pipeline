@Library('my-shared-library') _
pipeline {
    
    agent any
    parameters{

        choice(name:'action',choices:'create\ndelete',description:'choose create/destroy')
    }
    stages{
        
        stage ("Git checkout"){
            when { expression { params.action == 'create'}}
            steps{
                gitCheckout(
                    branch: "main",
                    url: "https://github.com/navedalisayyed/CICD-pipeline.git"
                )
                   

            }

        }
        stage ("MVN unit test"){
            when { expression { params.action == 'create'}}    
            steps{
               script{
                  mvnTest()
               }

            }

        }
        stage ("MVN integration test"){
            when { expression { params.action == 'create'}}    
            steps{
               script{
                  mvnIntegrationTest()
               }

            }
            
              
        }
        stage ("Static code analysis:sonarqube"){
            when { expression { params.action == 'create'}}    
            steps{
               script{
                   def SonarQubecredentialsId = 'sonar-api'
                   statiCodeAnalysis(SonarQubecredentialsId)
               }

            }
            
              
        }
        stage ("Qaulity gate status check:sonarqube"){
            when { expression { params.action == 'create'}}    
            steps{
               script{
                   def SonarQubecredentialsId = 'sonar-api'
                   QualityGateStatus(SonarQubecredentialsId)
               }

            }
            
              
        }
    }
}

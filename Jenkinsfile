@Library('my-shared-library') _
pipeline {
    
    agent any
    parameters{

        choice(name:'action',choices:'create\ndelete',description:'choose create/destroy')
        string(name: 'ImageName', description: "name of the docker build", defaultValue: 'javapp')
        string(name: 'ImageTag', description: "tag of the docker build", defaultValue: 'v1')
        string(name: 'DockerHubUser', description: "name of the Application", defaultValue: 'navedali')
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
        // stage ("Qaulity gate status check:sonarqube"){
        //     when { expression { params.action == 'create'}}    
        //     steps{
        //        script{
        //            def SonarQubecredentialsId = 'sonar-api'
        //            QualityGateStatus(SonarQubecredentialsId)
        //        }

        //     }
    
        // }
        stage ("Maven Build"){
            when { expression { params.action == 'create'}}    
            steps{
               script{

                   mvnBuild()
               }

            }
       
        }
         stage ("Docker Image Build"){
            when { expression { params.action == 'create'}}    
            steps{
               script{

                   dockerBuild("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
               }

            }
        }
         stage ("Docker Image scan:Trivy"){
            when { expression { params.action == 'create'}}    
            steps{
               script{

                   dockerImageScan("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
               }

            }
        }
        stage ("Docker Image Push:DockerHub"){
            when { expression { params.action == 'create'}}    
            steps{
               script{

                   dockerImagePush("${params.ImageName}","${params.ImageTag}","${params.DockerHubUser}")
               }

            }
        }
        
    }
}

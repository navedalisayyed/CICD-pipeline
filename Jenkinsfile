@Library('jenkins_shared_lib') _
pipeline {
    
    agent any

    stages{
        stage ("Git checkout"){
            steps{
                gitCheckout{
                    branch: "main",
                    url: "https://github.com/navedalisayyed/CICD-pipeline.git"
                  }
                   

                }
            
              
        }
    }
}

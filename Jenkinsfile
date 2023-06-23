@Library('my-shared-library') _
pipeline{
    agent any

    parameters{
        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create or destroy')

    }
        stages{
            stage('Git Checkout'){
                when { expression { params.action == 'create' } }
                steps{
                    script{
                        gitCheckout(
                         branch: 'main', 
                         url: 'https://github.com/DivyaMatt/divya_java_app.git'
                        )
                    }
                }
            }
            stage('Unit test maven'){
                when { expression { params.action == 'create' } }
                steps{
                    script{
                        mvnTest()
                    }
                }
            }
            stage('Integration test maven'){
                when { expression { params.action == 'create' } }
                steps{
                    script{
                        mvnIntegrationTest()
                    }
                }
            }
            stage('Static code analysis: Sonarqube'){
         when { expression {  params.action == 'create' } }
            steps{
               script{
                   
                   def SonarQubecredentialsId = 'sonarqube-api'
                   statiCodeAnalysis(SonarQubecredentialsId)
               }
            }
        }
        stage('Quality Gate Status Check : Sonarqube'){
         when { expression {  params.action == 'create' } }
            steps{
               script{
                   
                   def SonarQubecredentialsId = 'sonarqube-api'
                   QualityGateStatus(SonarQubecredentialsId)
               }
            }
        }
        stage('Maven Build : maven'){
         when { expression {  params.action == 'create' } }
            steps{
               script{
                   
                   mvnBuild()
               }
            }
        }
            
    }
}
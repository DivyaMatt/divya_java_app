@Library('my-shared-library') _
pipeline{
    agent any
        stages{
            stage('Git Checkout'){
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
                steps{
                    script{
                        mvnTest()
                    }
                }
            }
            stage('Integration test maven'){
                steps{
                    script{
                        mvnIntegrationTest()
                    }
                }
            }
        }
}
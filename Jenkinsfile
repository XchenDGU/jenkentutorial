'''CODE_CHANGES = getGitChanges()'''
def gv 
pipeline {
    agent any
    parameters{
        string(name:'VERSION',defaultValue:'',description:'version to deply on prod')
        choice(name:'VERSION',choices:['1.1.0','1.1.2'],description:'')
        booleanParam(name:'executeTests',defaultValue:true,description:'')
    }
    
    environment {
        NEW_VERSION = '1.3.0'
        SERVER_CREDENTIALS = credentials('server-credentials') 
    }

    stages {
        stage('init'){
            steps{
                script{
                    gv = load "script.groovy"
                }
            }
        }
        
        stage('build') {
            steps {
                script{
                   gv.buildApp()
                }
            }
        }
        stage('test'){
            when{
                expression{
                    params.executeTests
                }
            }
            steps{
               script{
                   gv.testApp()
               }
            }
        }
        stage('deploy'){
            steps{
                script{
                    gv.deployApp()
                }
                
            }
        }
        
    }
    post{
        always{
            echo 'End of execution'
        }
        failure{
            echo 'Execution failed'
        }
    }

}


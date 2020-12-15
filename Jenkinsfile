'''CODE_CHANGES = getGitChanges()'''

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
        stage('build') {
            
            steps {
                echo 'building the application...'
                echo "building version ${NEW_VERSION}"
            }
        }
        stage('test'){
            when{
                expression{
                    params.executeTests
                }
            }
            steps{
                echo 'testing the application...'
            }
        }
        stage('deploy'){
            steps{
                echo 'deploying the application..'
                withCredentials([
                    usernamePassword(credentialsId:'server-credentials',usernameVariable:USER,passwordVariable:PWD)
                ]){
                    bat "Show credential ${USER} ${PWD}"
                    bat "deploying version ${params.VERSION}"
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


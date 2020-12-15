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
        SERVER_CREDENTIALS = credentials('server-credential') 
    }
    tools{
        maven 'Maven'   
    }
    stages {
        stage('build') {
            '''
            when{
                expression{
                    env.BRANCH_NAME == 'dev' && CODE_CHANGES == true
                }
            }
            '''
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
                    usernamePassword(credentials:'server-credentials',usernameVariable:USER,passwordVariable:PWD)
                ]){
                    echo "some script ${USER} ${PWD}"
                    echo "deploying version ${params.VERSION}"
                }
            }
        }
        
    }
    post{
        always{
            
        }
        failure{
            
        }
    }

}


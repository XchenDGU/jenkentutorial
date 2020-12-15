#CODE_CHANGES = getGitChanges()

pipeline {
    agent any
    environment {
        NEW_VERSION = '1.3.0'
        SERVER_CREDENTIALS = credentials(server-credential'') #need credential plugin
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
                    bat "some script ${USER} ${PWD}"
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


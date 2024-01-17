pipeline {
    agent any
    
    environment {
        LAPTOP = "LENOVO"
        TENANT= "chris"
        branchName= env.BRANCH_NAME.toLowerCase().replaceAll('\\/','-')   
    }
    
    parameters {
        string(name: 'PROCESSOR', defaultValue: "intel")
        string(name: 'LAPTOP', defaultValue: "HP")
    }
    
    stages {
        stage('Hello') {
            steps {
                echo "${LAPTOP}"+"${PROCESSOR}"
                echo "${tenant}"
            }
        }
        
        stage('Approve deploying to prod') {
            when {
                expression {
                    branchName == /jenkins/
                }
            }
            steps {
                timeout(60) {
                    script{
                        Answer = input message: 'Deploy to production?', parameters:
                        [choice(choices: "yes\nNO", description: 'Are you SERIOUS?', name: 'choice')]
                    }
                }
            }
        }
    }
}

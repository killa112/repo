pipeline {
    agent any
    
    environment {
        LAPTOP = "LENOVO"
        TENANT= "chris"
        branchName= env.BRANCH_NAME.toLowerCase().replaceAll('\\/','-')
        buildNumber= env.BUILD_NUMBER
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
                echo 
            }
        }
        
        stage('UAT cluster') {
            when {
                expression {
                    branchName == /main/
                }
            }
            steps {
                echo "branch is ${branchName}"
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

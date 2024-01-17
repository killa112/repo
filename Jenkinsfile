pipeline {
    agent any
    
    environment {
        LAPTOP = "LENOVO"
        TENANT= "chris"
        branchName= env.BRANCH_NAME.toLowerCase().replaceAll('\\/','-')
        buildNumber= env.BUILD_NUMBER.toLowerCase()
    }
    
    parameters {
        string(name: 'PROCESSOR', defaultValue: "intel")
        string(name: 'LAPTOP', defaultValue: "HP")
    }
    
    stages {
        
        
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

        stage('Maven build'){
            steps{
                script {
                    def version = sh script: 'mvn help:evaluate -Dexpression=project.version -q -DforceStdout', returnStdout: true
                    majorVersion = version.substring(0,4)
                    
                    RELEASE_VER=majorVersion+env.BUILD_NUMBER+'-SNAPSHOT'
                    
                }
            }
        }

        stage('print all') {
            steps {
                echo "${LAPTOP}"+"${PROCESSOR}"
                echo "${tenant}"
                echo "${buildNumber}"
                echo "${RELEASE_VER}"
                echo "${majorVersion}"
            }
        }
    }
}

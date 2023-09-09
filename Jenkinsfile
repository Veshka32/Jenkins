pipeline {
    agent any
    parameters {
        string(name: 'Greeting', defaultValue: 'Hello', description: 'How should I greet the world?')
        string(name: 'email', description: 'send notification here')
        booleanParam(name: 'trigger', description: 'Trigger')

    }
    environment {
        USER_NAME = credentials('user_name')
    }
    stages {
        stage('Build') {
            steps {
                echo "${params.Greeting} ${USER_NAME}!"
                echo "Current build URL: ${currentBuild.absoluteUrl}"
            }
        }
        stage('Environments') {
            steps {
                echo 'this is a build number: ${BUILD_NUMBER}'
            }
        }
        stage('Condition') {
             when {
                 expression {
                    return params.trigger
                }
             }
             options {
                timeout(time: 5, unit:'SECONDS')
            }
            steps {
                input message: 'Proceed?'
                echo "Triggered"
            }
            post{
                success {
                    echo "Success"
                }
                aborted {
                    echo "Not success"
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
    post {
        always {
           script {
                if (params.email != null) {
                mail to: params.email, subject: 'Job is finished!', body: 'Oooops'
            }
           }
        }
    }
}

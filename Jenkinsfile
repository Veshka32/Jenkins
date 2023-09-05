pipeline {
    agent any
    parameters {
        string(name: 'Greeting', defaultValue: 'Hello', description: 'How should I greet the world?')
        string(name: 'email', description: 'send notification here')
        string(name: 'trigger', description: 'Trigger')

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
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Condition') {
             when {expression(params.trigger)}
            steps {
                echo "Triggered"
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

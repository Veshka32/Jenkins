pipeline {
    agent any
    parameters {
        string(name: 'Greeting', defaultValue: 'Hello', description: 'How should I greet the world?')
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
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}

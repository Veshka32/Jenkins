pipeline {
    agent any
    parameters
    environment {
        USER_NAME = credentials('user_name')
        DEMO = "Demo number is 1"
    }
    stages {
        stage('Stage name') {
            environment {
                STEP_ENV = "I'm an env inside stage 1"
            }
            steps {
                echo "$DEMO!"
                echo "User name is a secret: ${USER_NAME}"
                echo "User name is a secret: ${env.USER_NAME}"
                echo "$STEP_ENV"
            }
        }
        stage('Stage with input') {
            input {
                message 'What is you message?'
                ok 'Nice!'
                parameters {
                    string(name: 'MESSAGE', defaultValue: "I'm dump'", description: 'Type anything')
                }
            }
            steps {
                echo "This is your message: ${MESSAGE}"
            }
            parallel {
                stage('First') {
                    echo "I am first parallel"
                }
                stage('Second') {
                    echo "I am second parallel"
                }
            }
        }
        stage('Write file') {
            steps {
                writeFile file: "Testfile.txt", text: "Build name is $BUILD_NAME"
            }
        }
    }
    post {
        always {
            echo "I'm always printed"
            archivedArtifacts "Testfile.txt"
        }
    }
}

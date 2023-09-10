library remote: "https://github.com/Veshka32/Jenkins.git"

pipeline {
    agent any
    parameters {
        booleanParam(name: 'DO', defaultValue: false, description: 'Do action')
    }
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
        stage('Parameter') {
            when {
                expression {return params.DO}
            }
            steps {
                echo getParameter()
            }
        }
        stage('Stage with parallel stages') {
            parallel {
                stage('First') {
                    steps {
                        echo "$DEMO"
                    }
                }
                stage('Second') {
                    steps {
                        echo "$BUILD_NUMBER"
                    }
                }
            }
        }
        stage('Write file') {
            input {
                message 'What is you message?'
                ok 'Nice!'
                parameters {
                    string(name: 'MESSAGE', defaultValue: "I'm dump'", description: 'Type anything')
                }
            }
            steps {
                echo "This is your message: ${MESSAGE}"
                writeFile file: "Testfile.txt", text: "${MESSAGE}"
                script {
                    if (Math.random() > 0.5) {
                        throw new Exception()
                    }
                }
            }
        }
    }
    post {
        always {
            echo "I'm always printed"
            archiveArtifacts "Testfile.txt"
        }
        success {
            tools()
        }
        failure {
            echo "Exception has been thrown"
        }
    }
}

String getParameter() {
    return "I'm a parameter: $DO"
}

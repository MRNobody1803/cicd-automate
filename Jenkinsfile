pipeline {
    agent any

    parameters {
        choice(
            name: 'VERSION',
            choices: ['1.0.0', '1.1.0', '1.2.0', '1.3.0'],
            description: 'choose the version'
        )

        booleanParam(
            name: 'execute_tests',
            defaultValue: true,
            description: 'execute unit tests'
        )
    }

    stages {
        stage("init") {
            steps {
                script {
                    echo "initializing..."
                    // gv = load "script.groovy"
                }
            }
        }

        stage("test") {
            when {
                expression { params.execute_tests == true }
            }
            steps {
                script {
                    echo "executing unit tests"
                }
            }
        }

        stage("build") {
            when {
                expression { env.BRANCH_NAME == 'master' }
            }
            steps {
                script {
                    echo "building the application..."
                    echo "on branch ${env.BRANCH_NAME}"
                    // sh 'mvn package'
                }
            }
        }

        stage("deploy") {
            when {
                expression { env.BRANCH_NAME == 'master' }
            }
            steps {
                script {
                    echo "deploying on branch ${env.BRANCH_NAME}"
                    echo "version is ${params.VERSION}"

                    // withCredentials([usernamePassword(credentialsId: 'server-credentials', passwordVariable: 'PWD', usernameVariable: 'USER')]) {
                    //     sh 'echo Deploying to server with user $USER and password $PWD'
                    // }

                    // gv.deployApp()
                }
            }
        }
    }
}

def gv

pipeline {
    agent any

    environment {
        NEW_VERSION = '1.3.0'
        SERVER_CREDENTIALS = credentials('server-credentials')
    }

    tools {
        maven 'Maven-3.9'
        // jdk 'jdk-11'
    }

    parameters {
        // string(name: 'NEW_VERSION', defaultValue: '1.0.0', description: 'new version')
        credentials(name: 'SERVER_CREDENTIALS', defaultValue: 'server-credentials', description: 'server credentials')

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
                    gv = load "script.groovy"
                }
            }
        }

        stage("build jar") {
            steps {
                script {
                    echo "building jar"
                    echo "new version is ${NEW_VERSION}"
                    gv.buildJar()
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    echo "building image"
                    gv.buildImage()
                }
            }
        }

//         stage("build") {
//             steps {
//                 script {
//                     echo "building the application..."
//                     // sh 'mvn package'
//                 }
//             }
//         }

        stage("test") {
            when {
                expression { return params.execute_tests == true }
            }
            steps {
                script {
                    echo "executing unit tests"
                }
            }
        }

        stage("deploy") {
            steps {
                script {
                    echo "deploying"
                    echo "version is ${params.VERSION}"
                    echo "server credentials are ${SERVER_CREDENTIALS}"

                    withCredentials([usernamePassword(credentialsId: 'server-credentials', passwordVariable: 'PWD', usernameVariable: 'USER')]) {
                    //     echo "username is ${USER}"
                    //     echo "password is ${PASS}"
                    // }

                    // gv.deployApp()
                }
            }
        }
    }
}


// pipeline {
//     agent any
//     environment {
//         NEW_VERSION = '1.3.0'
//         SERVER_CREDENTIALS = credentials('server-credentials')    }
//     tools {
//         maven : 'Maven'
//         //jdk 'jdk-11'
//     }
//     parameters {
//         //string(name: 'NEW_VERSION', defaultValue: '1.0.0', description: 'new version')
//         //credentials(name: 'SERVER_CREDENTIALS', defaultValue: 'server-credentials', description: 'server credentials')
//         choice(name: 'VERSION', choices: ['1.0.0', '1.1.0', '1.2.0', '1.3.0'], defaultValue: true, description: 'choose the version')
//         booleanParam(name: 'execute_tests', defaultValue: true, description: 'execute unit tests')
//     }
//     stages {
//         stage("init") {
//             steps {
//                 script {
//                     //gv = load "script.groovy"
//                     echo "initializing..."
//                 }
//             }
//         }

//         stage("build") {
//             steps {
//                 script {
//                     echo "building the application..."
//                     //sh 'mvn package'
//                 }
//             }
//         }
//         stage("test") {
//             when {
//                 expression { return params.execute_tests == true }
//             }
//             steps {
//                 script {
//                     echo "executing unit tests"
//                 }
//             }
//         }
//         stage("deploy") {
//             steps {
//                 script {
//                     echo "deploying"
//                     echo "version is ${params.VERSION}"
// //                   echo "server credentials are ${SERVER_CREDENTIALS}"
// //                     withCredentials([usernamePassword(credentialsId: 'server-credentials', passwordVariable: 'PWD', usernameVariable: 'USER')]) {
// //                         echo "username is ${USER}"
// //                         echo "password is ${PASS}"
// //                     }
//                     //gv.deployApp()
//                 }
//             }
//         }
//     }
// }
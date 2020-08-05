pipeline {
    agent any
    tools {nodejs "nodejs-server"}
    environment {
        CI = 'true'
    }
    stages {
        stage('Verificar qualidade do código') {
            steps {
                script {
                    def scannerHome = tool 'sonarqubescanner';
                    sh "echo ${scannerHome}"
                    sh "${tool("sonarqubescanner")}/bin/sonar-scanner --help"
                }
            }
        }
        stage("Instalar depedências") {
            steps {
                script {
                    def nodeHome = tool 'nodejs-server';
                    sh "echo ${nodeHome}"
                }
                nodejs(nodeJSInstallationName: 'nodejs-server'){
                    sh "npm install"
                }
            }
        }

        stage("Testes unitários") {
            steps {
                nodejs(nodeJSInstallationName: 'nodejs-server'){
                    sh "npm test"
                }
            }
        }
    }
}



// pipeline {
//     agent {
//         docker {
//             image 'node:6-alpine'
//             args '-p 3000:3000'
//         }
//     }
//     environment {
//         CI = 'true'
//         HOME = '.'
//     }
//     stages {
//         stage('Test') {
//             environment {
//                 scannerHome = tool 'sonarqubescanner'
//             }
//             steps {
//                 withSonarQubeEnv('sonarqubeserver') {
//                     sh "ls"
//                     sh "echo ${scannerHome}"
//                     sh "${tool("sonarqubescanner")}"
//                     sh "${tool("sonarqubescanner")}/bin/sonar-scanner \
//                         -Dsonar.host.url=http://10.11.73.5:9000 \
//                         -Dsonar.projectKey=simple-api-teste \
//                         -Dsonar.projectName=SimpleAPI \
//                         -Dsonar.projectVersion=1.0 \
//                         -Dsonar.sources=src \
//                         -Dsonar.exclusions=node_modules/**, coverage/**, public/**, build/**, **/__tests__/** \
//                         -Dsonar.sourceEncoding=UTF-8 \
//                         -Dsonar.javascript.lcov.reportPaths=__tests__/coverage/lcov.info \
//                         -Dsonar.login=226b26692118a8dd4fe8dd7c2d908307c40c6095 \
//                     "
//                 }
//             }
//         }

//         stage("Install Dependencies") {
//             steps {
//                 sh "npm install"
//             }
//         }

//         stage("Testes unitários") {
//             steps {
//                 sh "npm test"
//             }
//         }
//     }
//         // stage('Quality Gate status check'){
//         //     steps{
//         //         script{
//         //             withSonarQubeEnv('sonarqubeserver'){
//         //                 timeout(time: 1, unit:'HOURS'){
//         //                     def qg = waitForQualityGate()
//         //                     if (qg.status != 'OK'){
//         //                         error "Pipeline aborted due to quality gate failure: ${qg.status}"
//         //                     }
//         //                 }
//         //             }
//         //         }
//         //     }

//         // }
//         // stage('Test') {
//         //     steps {
//         //         sh './jenkins/scripts/test.sh'
//         //     }
//         // }
//         // stage('Deliver') {
//         //     steps {
//         //         sh './jenkins/scripts/deliver.sh'
//         //         input message: 'Finished using the web site? (Click "Proceed" to continue)'
//         //         sh './jenkins/scripts/kill.sh'
//         //     }
//         // }
// }

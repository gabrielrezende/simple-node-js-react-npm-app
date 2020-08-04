pipeline {
    agent any
    tools {nodejs "nodejs-server"}
    stages {
        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    // def scannerHome = tool 'sonarqube';
                    withSonarQubeEnv("sonarqube-container") {
                        sh "${tool("sonarqube-container")}/bin/sonar-scanner \
                            -Dsonar.projectKey=test-node-js \
                            -Dsonar.sources=. \
                            -Dsonar.css.node=. \
                            -Dsonar.host.url=http://127.0.0.1:9000 \
                            -Dsonar.login=226b26692118a8dd4fe8dd7c2d908307c40c6095"
                    }
                }
           }
        }
   
        stage("Install Project Dependencies") {
            steps {
                nodejs(nodeJSInstallationName: 'nodejs-server'){
                    sh "npm install"
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
//     }
//     stages {
//         stage('Build') {
//             steps {
//                 sh 'npm install'
//             }
//         }
//         stage('Quality Gate status check'){
//             steps{
//                 script{
//                     withSonarQubeEnv('SonarServer'){
//                         timeout(time: 1, unit:'HOURS'){
//                             def qg = waitForQualityGate()
//                             if (qg.status != 'OK'){
//                                 error "Pipeline aborted due to quality gate failure: ${qg.status}"
//                             }
//                         }
//                     }
//                 }
//             }

//         }
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
//     }
// }

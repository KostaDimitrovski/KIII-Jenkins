// node {
//     def app
//     stage('Clone repository') {
//         checkout scm
//     }
//     stage('Build image') {
//        app = docker.build("kostadimitrovski/kiii-jenkins")
//     }
//     stage('Push image') {   
//         docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
//             app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
//             app.push("${env.BRANCH_NAME}-latest")
//             // signal the orchestrator that there is a new version
//         }
//     }
// }
pipeline {
    agent any
    
    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }
        
        stage('Build and push Docker image') {
            when {
                branch 'dev'
            }
            steps {
                script {
                    def app = docker.build("kostadimitrovski/kiii-jenkins")
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        app.push("${env.BRANCH_NAME}-latest")
                    }
                }
            }
        }
    }
}


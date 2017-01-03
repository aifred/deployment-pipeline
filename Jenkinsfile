#!groovy

node {
    stage('Build') {
        node {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], 
                userRemoteConfigs: [[credentialsId: 'Aifred_Git', url: 'http://git/ongsa/DeploymentPipeline.git']]])
            sh 'npm install'
            sh 'npm run build.prod' 
        }
    }

    stage('Test') {
    }

    stage('Deploy') {
    }
}
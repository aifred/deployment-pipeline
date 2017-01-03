#!groovy

node {
    stage('Build') {
        node {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], 
                userRemoteConfigs: [[credentialsId: 'Aifred_Git', url: 'http://git/ongsa/DeploymentPipeline.git']]])
            
            echo 'Fetching 3rd party dependencies'
            sh 'npm install'
            
            echo 'Performing Unit Testing'
            sh 'npm test'
            
            echo 'Performing Component Test'
            sh 'npm install webdriver-manager'
            sh 'npm run webdriver-update'
            sh 'npm run webdriver-start'
            sh 'npm run e2e'

            echo 'Compiling source code'
            sh 'npm run build.prod' 
            echo 'Distribution Package ${} is created.'
        }
    }

    stage('Test') {
    }

    stage('Deploy') {
    }
}
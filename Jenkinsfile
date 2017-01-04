#!groovy

node {
    stage('Build') {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], 
                    userRemoteConfigs: [[credentialsId: 'Aifred_Git', url: 'http://git/ongsa/DeploymentPipeline.git']]])
        parallel(
           "stream 1" : {
               node {
                    echo 'Fetching 3rd party dependencies'
                    sh 'npm install'
                    
                    echo 'Performing Unit Testing'
                    sh 'npm test'
                    
                    echo 'Performing Component Test'
                    // TODO: Integrate e2e test

                    echo 'Compiling source code'
                    sh 'npm run build.prod' 
                    echo 'Distribution folder is created.'
                }
           },
           "stream 2" : {
               node {
                   echo 'Code Linting'
                   sh 'sonarlint'

                   echo 'Static Code Analysis'
                   sh 'sonar-scanner'
               }
           }
       ) 
    }

    stage('Test') {
    }

    stage('Deploy') {
    }
}
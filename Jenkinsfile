#!groovy

node {
    stage('Build') {
        // checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], 
        //             userRemoteConfigs: [[credentialsId: 'Aifred_Git', url: 'http://git.fpprod.corp/ongsa/DeploymentPipeline.git']]])
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
                    sh 'sonarlint --src "src/**"'

                    echo 'Static Code Analysis'
                    def scannerHome = tool name: 'SonarQube Scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                    withSonarQubeEnv {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                    // sh 'sonar-scanner -Dproject.settings=./sonar-project.properties'
               }
           }
       ) 
    }

    stage('Test') {
    }

    stage('Deploy') {
    }
}
node ('') {
    timestamps {
        
            step([$class: 'WsCleanup'])
            stage('Checkout code') {
                checkout scm
            }
           
            stage('Build & Deployment') {
                def k8sImage = docker.image('shridhanr/androidapp:latest')
                k8sImage.inside("-u 0:0 --entrypoint=''"){
                          sh "npm cache clean --force"
                          //sh "rm -rf node_modules" 
                          sh "npm install --global yarn"
                          sh "yarn install"
                          sh "yarn add @react-native-community/cli-platform-android@3.0.3"
                          sh "npm install"     
                          sh "npm audit fix --force"
                          sh "npm update"
                          sh "yarn add react-native@0.61.5"
                          sh "chmod -R 777 /root/"
                          sh './gradlew clean'
                          sh "bundle install"
                          sh "fastlane distribute version_code:1000$BUILD_NUMBER store_password:$KEYSTORE_PASSWORD key_alias:$KEYWORD_ALIAS"

                    
                  }
                   
            }
    }
 }


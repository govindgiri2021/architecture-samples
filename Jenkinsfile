node ('') {
    timestamps {
        
            step([$class: 'WsCleanup'])
            stage('Checkout code') {
                checkout scm
            }
           
            stage('Build & Deployment') {
                def k8sImage = docker.image('govndgiri2021/androidapp:latest')
                k8sImage.inside("-u 0:0 --entrypoint=''"){
                          sh "yarn add @react-native-community/cli-platform-android@3.0.3"
                          sh "yarn add react-native@0.61.5"
                            
                          sh "chmod -R 777 /root/"
                          sh './gradlew clean'
                          sh "bundle install"
                          sh "fastlane distribute version_code:1000$BUILD_NUMBER store_password:$KEYSTORE_PASSWORD key_alias:$KEYWORD_ALIAS"
                    
                }
                   
            }
    }
 }

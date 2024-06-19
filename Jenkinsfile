#!/usr/bin/env groovy

// library identifier: 'jenkins-shared-library@master', retriever: modernSCM(
//         [$class: 'GitSCMSource',
//          remote: 'https://github.com/quancyber/jenkins-shared-library.git',
//          credentialsId: 'github-credentials'
//         ]
// )

@Library('jenkins-shared-library')

def gv

pipeline {
    agent any
    tools {
        maven 'apache-maven-3.9.7'
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                    buildJar()
                }
            }
        }
        stage("build and push image") {
            steps {
                script {
                    buildImage 'quancyber/demo-app:3.0'
                    dockerLogin()
                    dockerPush 'quancyber/demo-app:3.0'
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    gv.deployApp()
                }
            }
        }
    }
}

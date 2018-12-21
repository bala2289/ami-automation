#!/usr/bin/env groovy
pipeline {
    agent any
    stages {
        stage('pipeline start') {
            steps {
                sh 'echo "pipeline initiated.."'
            }
        }
        stage('packer validate template') {
            steps {
                sh 'chmod +x packer'
                sh 'pwd'
                sh './packer validate create-ami.json'
                }
        }
        stage('packer build AMI') {
            steps {
                sh 'pwd'
                sh './packer build create-ami.json'
                sh 'cat manifest.json |grep ami|awk -F ":" \'{print $NF}\'|tr -d \",'
            }
        }
    
    }
    post { 
        always { 
            echo 'Cleaning up..'
            sh 'rm manifest.json'
        }
    }
}
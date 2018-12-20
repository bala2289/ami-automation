#!/usr/bin/env groovy
pipeline {
    agent any
    stages {
        stage('pipeline start') {
            steps {
                sh 'echo "pipeline initiated.."'
                sh 'rm -r ami-automation'
            }
        }
        '''stage('Clone repository') {
            steps {
                sh 'git clone https://github.com/bala2289/ami-automation.git'
                sh 'cd ami-automation'
                }
        }'''

        stage('packer validate template') {
            steps {
                sh 'chmod +x packer'
                sh './packer validate create-ami.json'
                }
        }
        stage('packer build AMI') {
            steps {
                sh './packer build create-ami.json'
                sh 'echo ami-id:`cat manifest.json | jq -r \'.builds[-1].artifact_id\' |  cut -d\':\' -f2`'
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
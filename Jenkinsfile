pipeline {
    agent any
    tools {
        maven 'maven3'
        jdk 'java17'
    }
    stages {
        stage('download-git-code') {
            steps {
            echo "download code from git"
            git branch: 'main', url: 'https://github.com/UsamaSatte/maven-jenkins4'
            }
        }
        stage('build') {
            steps {
            echo "build java project using maven"
            sh 'mvn clean package'
            }
        }
        stage('archive-artifact') {
            steps {
            echo "archiving the artifacts"
            archiveArtifacts artifacts: '**/*.war', followSymlinks: false
            }
        }
        stage('trigger-deploy-job') {
            steps {
            echo "triggering deploy job"
            build wait: false, job: 'deployment'
            }
        }        
    }
}

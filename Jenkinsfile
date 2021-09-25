pipeline {
    agent any
    tools {
        maven 'maven382'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('GitHub'){
            steps{
                git branch: 'main', url: 'https://github.com/vsaini1/nexus-simple1'
            }
        }
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'simple-app', classifier: '', file: 'target/simple-app-1.0.0.war', type: 'war']], credentialsId: 'nexus-ul', groupId: 'in.javahome', nexusUrl: '10.177.89.240:32000', nexusVersion: 'nexus3', protocol: 'http', repository: 'simpleapp-release', version: '1.0.0'
            }}}}

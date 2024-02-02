pipeline {
 environment {
 imagename = "bondugulaavinash/jenkins-docker"
 registryCredential = 'bondugulaavinash'
 dockerImage = ''
 }
 agent any
 stages {
 stage('Cloning Git') {
 steps {
 git([url: 'https://github.com/BondugulaAvinash/jenkinstest.git', branch: 'main'])
 }
 }
 stage('Building image') {
 steps{
 script {
 dockerImage = docker.build imagename
 }
 }
 }
 stage('Running image') {
 steps{
 script {
 sh "docker run -itd -P ${imagename}:latest"
 }
 }
 }
 stage('Deploy Image') {
 steps{
 script {
 docker.withRegistry( '', registryCredential ) {
 dockerImage.push("$BUILD_NUMBER")
 dockerImage.push('latest')
 }
 }
 }
 }
 }
}

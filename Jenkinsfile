#!groovy
def rev 
node('jenkins') {
  stage('Checkout') {
    checkout scm
    rev  = "$BUILD_NUMBER"
  }

  stage('Syntax') {
    sh "true"
  }

  stage('Build') {
    sh "true"
  }

  stage('Deploy') {
    sh "tru"
  }
 
  stage('Test') {
    sh "true"
  }

 stage('Approve') {
    echo  "${rev}: Waiting for approval for change"
    input "Do you want to upload the image to pre-prod/prod environment?"
    sh "true"
  }

  stage('Publish') {

  }
}

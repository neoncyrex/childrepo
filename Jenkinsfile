#!groovy
def rev 
node('jenkins') {
  stage('Checkout') {
    checkout scm
    rev = "$BUILD_NUMBER"
  }

  stage('Syntax') {
    sh "true"
  }

  stage('Build') {
    sh "true"
  }

  stage('Deploy') {
    sh "true"
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
	sh "mkdir -p ../build${rev}"
	sh "cd ../build${rev}; git clone git@github.com:neoncyrex/example.git"
	sh "cp -r * ../build${rev}/example/vsrx_build_automation"
        sh "cd ../build${rev}/example; git add .; git commit -m 'Jenkins build $rev';USER=neoncyrex git push origin master "
  }
}


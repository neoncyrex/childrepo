#!groovy
def rev 
node('jenkins') {
  stage('Checkout') {
    checkout scm
    rev = "$BUILD_NUMBER"
    repodir = getrepodir('git@github.com:neoncyrex/example.git')
    echo ${repodir}
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
    push_repo_to_subdirectory("git@github.com:neoncyrex/example.git")
    sh "true"
  }

 stage('Approve') {
    echo  "${rev}: Waiting for approval for change"
    input "Do you want to upload the image to pre-prod/prod environment?"
    sh "true"
  }

  stage('Publish') {
	sh "mkdir -p ../build${rev}"
	sh "cd ../builds/build${rev}; git clone git@github.com:neoncyrex/example.git"
	sh "cd ../builds/build${rev}/example; git checkout -b jenkins"
	sh "cp -r * ../builds/build${rev}/example/vsrx_build_automation"
        sh "cd ../builds/build${rev}/example; git add .; git commit -m 'Jenkins build $rev';git push origin jenkins"
	sh "rm -rf ../builds/build${rev}/example"
  }
}

def getrepodir(repo) {     
  def matcher = repo =~ '/([^/]+).git'     
  matcher ? matcher[0][1] : null 
}



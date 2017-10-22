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
	def repo = 'git@github.com:neoncyrex/example.git'
        publish_repo_to_subdirectory(repo,'vsrx_build_automation','jenkins')
  }
}


def publish_repo_to_subdirectory(destrepo,subdirectory,branch) {
   def repodir = getrepodir(destrepo)
   sh "mkdir -p ../builds/build${rev}"
   sh "cd ../builds/build${rev}; git clone ${destrepo}"
   sh "cd ../builds/build${rev}/${repodir}; git checkout -b ${branch}"
   sh "cp -r * ../builds/build${rev}/${repodir}/${subdirectory}"
   sh "cd ../builds/build${rev}/${repodir}; git add .; git commit -m 'Jenkins build $rev';git push origin ${branch}"
   sh "rm -rf ../builds/build${rev}/${repodir}"
}

def getrepodir(repo) {
   def matcher = repo =~ '/([^/]+).git'
   matcher ? matcher[0][1] : null
}



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
        publish_repo_to_subdirectory(repo,'vsrx_build_automation','jenkins', rev)
  }
}


def publish_repo_to_subdirectory(destrepo,subdirectory,branch,buildnumber) {
   def repodir = getrepodir(destrepo)
   sh "mkdir -p ../builds/build${buildnumber}"
   sh "cd ../builds/build${buildnumber}; git clone ${destrepo}"
   sh "cd ../builds/build${buildnumber}/${repodir}; git checkout -b ${branch}"
   sh "cp -r * ../builds/build${buildnumber}/${repodir}/${subdirectory}"
   sh "cd ../builds/build${buildnumber}/${repodir}; git add .; git commit -m 'Jenkins build $buildnumber';git push origin ${branch}"
   sh "rm -rf ../builds/build${buildnumber}/${repodir}"
}

def getrepodir(repo) {
   def matcher = repo =~ '/([^/]+).git'
   matcher ? matcher[0][1] : null
}



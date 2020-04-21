pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr:'5', artifactNumToKeepStr:'5', artifactDaysToKeepStr:'7'))
    durabilityHint('PERFORMANCE_OPTIMIZED')
    retry(1)
    skipDefaultCheckout()
    timestamps()
  }
  stages {
    stage ('Checkout') {
      steps {
        checkout([$class:'GitSCM', branches:[[name:'*/*']], doGenerateSubmoduleConfigurations:false, extensions:[], submoduleCfg:[], userRemoteConfigs:[[credentialsId:'github', url:'https://github.com/samfil-technohub/samfil-technohub-landingpage-app.git']]])
        stash(name: 'ws', includes: '**', excludes: '**/.git/**')
        echo "Project Checked Out"        
      }
    }
    stage ('Build') {
      steps {
        unstash 'ws'
        echo "Building App"
      }
    }
    stage ('Test') {
      steps {
        unstash 'ws'
        echo "Testing App"
      }
    }
    stage('Deploy') {
      when {
        branch 'master' 
      }
      steps {
          echo "Deploying to Production"
      }
    }
  }
  post {
    success {
      echo "Succeeded"
    }
    failure {
      echo "Failed!!"
    }
  }
}
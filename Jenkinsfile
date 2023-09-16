pipeline {
  agent any 
  tools {
    maven 'M2_HOME'
        }
stages {
  stage ('Git checkout') {
    steps {
      git 'https://github.com/KunalSawant29/star-agile-insurance-project.git'
    }
  }

  stage ('Build') {
    steps {
      sh 'mvn clean package'
    }
  }

  stage ('Publish HTML reports') {
    steps {
      publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/Insure-me-project/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
    }
  }

  stage ('Docker Build') {
    steps {
      sh 'docker build -t kunalsawant29/insure-me-project:1.0 .'
    }
  }

  stage ('Push Docker image to Dockerhub') {
    steps {
      withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
      sh 'docker login -u kunalsawant29 -p ${dockerhubpwd}'
}
      sh 'docker push kunalsawant29/insure-me-project:1.0'
    }
  }
    }
}
    
    




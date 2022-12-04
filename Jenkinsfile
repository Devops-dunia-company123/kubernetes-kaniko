pipeline {

  options {
    ansiColor('xterm')
  }

  agent {
    kubernetes {
      yamlFile 'pod-git.yaml'
    }
  }
    
 
      
  stage('Get a Maven project') {
      git url: 'https://github.com/Devops-dunia-company123/kubernetes-kaniko', branch: 'main'
      container('maven') {
        stage('Build a Maven project') {
          sh '''
          echo pwd
          '''
        }
      }
    }

    stage('Build Java Image') {
      container('kaniko') {
        stage('Build a Go project') {
          sh '''
            /kaniko/executor --context `pwd` --destination duniaalk/hello-kaniko:1.0
          '''
        }
      }
    }

  }


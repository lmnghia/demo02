pipeline {
  agent any
  stages {
    stage('Git Checkout') {
      parallel {
        stage('Git Checkout') {
          steps {
            git 'https://github.com/tsheth/DockerbaseDSSC.git'
          }
        }
        stage('Static code analysis') {
          steps {
            sh '''echo "static code analysis for github code"
sleep 12'''
          }
        }
      }
    }
    stage('Build Docker image') {
      parallel {
        stage('Build Web Service') {
          steps {
            sh '''echo "docker build command"
sleep 10'''
          }
        }
        stage('Build Location service') {
          steps {
            sh '''echo "docker build cluster image"
sleep 10'''
          }
        }
        stage('Build Clustering service') {
          steps {
            sh 'echo "Docker build -t <source image> <destination image>'
          }
        }
      }
    }
    stage('Local Test') {
      parallel {
        stage('Local Test') {
          steps {
            sh '''echo "local testing results"
sleep 10'''
          }
        }
        stage('DSSC Security Test') {
          steps {
            sh '''echo "send message to github issue"
sleep 15'''
          }
        }
      }
    }
    stage('Classify image tag') {
      steps {
        sh '''echo "docker tag to classify image"
sleep 5'''
      }
    }
    stage('Push image to staging') {
      steps {
        sh '''echo "ECR registry push for image"
sleep 10'''
      }
    }
    stage('Deploy to Staging') {
      steps {
        sh '''echo "ECS deploy commands"
sleep 10'''
      }
    }
    stage('Manual Test Success?') {
      steps {
        input 'Deployment Approval based on manual testing'
      }
    }
    stage('Classify image for production') {
      steps {
        sh '''echo "tag image with production ready build"
sleep 10'''
      }
    }
    stage('Approve for production deploy') {
      steps {
        input 'Approved for production deploy'
      }
    }
    stage('Deploy to production') {
      steps {
        sh '''echo "ECS commands to deploy service to production"
sleep 10'''
      }
    }
  }
}
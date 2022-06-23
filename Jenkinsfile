pipeline{
  agent {
    docker {
      image 'builder'
    }
  }

  stages {
    stage ('git clone') {
      steps {
        git 'https://github.com/ww-insight/devops-edu-11-boxfuse.git'
      }
    }
    stage ('build war artifact') {
      steps {
        sh 'mvn package'
      }
    }
    stage ('build container') {
      steps {
        sh 'docker build -t wwbel/boxfuse .'
      }
    }
    stage ('push container') {
      steps {
        sh 'docker push wwbel/boxfuse'
      }
    }
  }

}
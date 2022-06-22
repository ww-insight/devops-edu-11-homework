pipline{
  agent {
    docker {
      image '10.129.0.9:4242/edu-11-homework-buider'
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
        sh 'docker build wwbel/boxfuse'
      }
    }
    stage ('push container') {
      steps {
        sh 'docker push wwbel/boxfuse'
      }
    }
  }

}
pipeline{
  agent {
    docker {
      image 'builder'
      args '-v /var/run/docker.sock:/var/run/docker.sock --user root'
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
        withCredentials([usernamePassword(credentialsId: 'docker_hub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
           sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
        }
        sh 'docker push wwbel/boxfuse'
      }
    }
    stage ('up container') {
      steps{
        sshagent(['583788ca-55d0-48eb-9a55-5f5335c473a7']) {
          sh '''
                [ -d ~/.ssh ] || mkdir ~/.ssh && chmod 0700 ~/.ssh
                ssh-keyscan -t rsa,dsa 10.129.0.4 >> ~/.ssh/known_hosts
                ssh root@10.129.0.4 'docker ps --filter "ancestor=wwbel/boxfuse" -q | xargs docker stop && docker pull wwbel/boxfuse && docker run -d -p 8080:8080 wwbel/boxfuse'
          '''

        }
      }
    }
  }

}
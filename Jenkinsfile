pipeline {
  agent any
  stages {
    stage('Quality Gate Statuc Check') {
      agent any
      steps {
        script {
          sh "mvn clean install"
        }

      }
    }

    stage('build') {
      steps {
        script {
          sh 'cp -r ../devops-training@2/target .'
          sh 'docker build . -t sundardockerdevops/devops-training:$Docker_tag'
          withCredentials([string(credentialsId: 'docker_pwd', variable: 'docker_pwd')]) {

            sh 'docker login -u sundardockerdevops -p $docker_pwd'
            sh 'docker push sundardockerdevops/devops-training:$Docker_tag'
          }
        }

      }
    }

  }
  environment {
    Docker_tag = getDockerTag()
  }
}
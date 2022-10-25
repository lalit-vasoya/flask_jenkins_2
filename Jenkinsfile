pipeline {
  agent any
  stages {
    agent {label "Local-Docker"}
    stage("Build"){
      steps {
        sh 'docker-compose up --build -d'
      }
    }
    stage("Static code anlysis"){
      steps {
        sh 'docker exec -i flask-practice bash -c "flake8"'  
      }
    }
  }
  // stages {
  //   stage("test"){
  //     steps {
  //       echo "testing the application"  
  //     }
  //   }
  // }
}

pipeline {
  agent any
  stages {
    stage("Build"){
      agent {label "Local-Docker"}
      steps {
        sh 'docker-compose up --build -d'
      }
    }
    stage("Static code anlysis"){
      agent {label "Local-Docker"}
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

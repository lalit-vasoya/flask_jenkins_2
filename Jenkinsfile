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
    stage("Test"){
      agent {label "Local-Docker"}
      steps {
        echo "Testing"
        sh 'docker exec -i flask-practice bash -c "pytest"'
      }
    }
  }
  post{
    always{
      echo 'Docker stop application!'
      sh 'docker-compose down'
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

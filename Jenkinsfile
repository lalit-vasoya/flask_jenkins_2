pipeline {
  agent {label "Local-Docker"}
  stages {
    stage("Build"){
      steps {
        sh 'yes | docker-compose up --build -d'
      }
    }
    stage("Static code anlysis"){
      steps {
        sh 'docker exec -i flask-practice bash -c "flake8"'  
      }
    }
    stage("Test"){
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

pipeline {
  agent {label "local-docker"}
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
    stage("Deploy"){
      agent {label "local-server"}
      steps {
        sh 'pwd'
        sh 'docker-compose up --build -d'
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

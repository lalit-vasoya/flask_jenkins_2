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
        sh 'docker-compose down && docker-compose up --build -d'
      }
    }
  }
  post{
    always{
      echo 'Docker stop application!'
      sh 'docker-compose down'
      sendNotificationByEmail()
    }
  }
}

def sendNotificationByEmail(){
    emailext (
        attachLog: true,
        subject: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
        body: """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
            <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
        recipientProviders: [developers(), buildUser()],
        to: "${env.ghprbActualCommitAuthorEmail}"
    )
}

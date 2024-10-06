pipeline{
    agent {
    label 'docker'
    }

    stages{
    stage("Starting Selenium Grid"){
    steps{
          sh "docker-compose up"

    }
      }


    stage("Bringing down grid"){
    steps{
          sh "docker-compose down"

    }
      }

}






pipeline{
    agent {
    label 'docker'
    }

    stages{

    stage("Starting Selenium Grid"){
    steps{
          sh "docker-compose -f grid.yaml up -d"
          sh "docker-compose -f test-suites.yaml up"
    }
      }


    stage("Bringing down grid"){
    steps{
          sh "docker-compose -f grid.yaml down"
          sh "docker-compose -f test-suites.yaml down"

    }
      }

}
}





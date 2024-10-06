pipeline{
    agent {
    label 'docker'
    }

    parameters {
      choice choices: ['chrome', 'firefox'], description: 'Please select browser to run test', name: 'BROWSER'
    }

    stages{

    stage("Starting Selenium Grid"){
    steps{
          sh "docker-compose -f grid.yaml up --scale ${params.BROWSER}=2 -d"
          sh "docker-compose -f test-suites.yaml up"
    }
      }


    stage("Bringing down grid"){
    steps{
          sh "docker-compose -f grid.yaml down"
          sh "docker-compose -f test-suites.yaml down"
          archiveArtifacts artifacts: './result/flight-reservation/emailable-report.html', followSymlinks: false
          archiveArtifacts artifacts: './result/vendor-portal/emailable-report.html', followSymlinks: false
    }
      }

}
}





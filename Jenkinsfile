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
          script{
          if( (fileExists('result/flight-reservation/testng-failed.xml'))|| (fileExists('result/vendor-portal/testng-failed.xml') ) ){
            error('failed tests found')
          }
          }
    }
      }


    stage("Bringing down grid"){
    steps{
          sh "docker-compose -f grid.yaml down"
          sh "docker-compose -f test-suites.yaml down"
          archiveArtifacts artifacts: 'result/flight-reservation/emailable-report.html', followSymlinks: false
          archiveArtifacts artifacts: 'result/vendor-portal/emailable-report.html', followSymlinks: false
    }
      }

}
}

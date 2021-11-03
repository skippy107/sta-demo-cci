pipeline{
    agent {
      docker {
        image 'skippy107/cumulusci:latest'
        args '-v ${WORKSPACE}:/usr/src/app -v /var/keys/cci:/home/docker/.cumulusci -v /var/keys/sfdx:/home/docker/.sfdx -v /var/keys/certs:/home/docker/.certs'
      }
    }
    stages {
      stage('Test') {
        steps {
          sh 'export HOME=/home/docker; . $HOME/.profile; $HOME/runtests.sh'
          //archiveArtifacts "robot/sta4/results/*"
          publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'robot/sta4/results', reportFiles: 'report.html', reportName: 'Test Results', reportTitles: ''])
        }
      }
    }
    post {
      failure {
        // archiveArtifacts "robot/sta4/results/*"
        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'robot/sta4/results', reportFiles: 'report.html', reportName: 'Test Results', reportTitles: ''])
      }
    }

}
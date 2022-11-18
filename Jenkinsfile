pipeline{
    agent any

    environment {
    CI = true
    ARTIFACTORY_ACCESS_TOKEN = credentials('az-docker-artifactory-token')
  }

  stages{
    stage ("maven build"){
        steps{
            sh 'mvn clean package'
        }
    }
  }
}
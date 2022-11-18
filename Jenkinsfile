pipeline{
    agent any
    tools{
        maven 'MAVEN_HOME'
        docker 'org.jenkinsci.plugins.docker.commons.tools.DockerTool'
    }

    environment {
        CI = true
        ARTIFACTORY_ACCESS_TOKEN = credentials('az-container-artifactory-token')
    }

    stages{
        stage ("maven build"){
            steps{
                sh 'mvn clean package'
            }
        }

        stage ("upload to artifactory"){
            agent {
                docker {
                    image 'releases-docker.jfrog.io/jfrog/jfrog-cli-v2:2.2.0' 
                    reuseNode true
                }
            }

            steps {
                sh 'jfrog rt upload --url http://10.0.0.0:9092/artifactory/ --access-token ${ARTIFACTORY_ACCESS_TOKEN} com/* restro-maven-local/'
            }

        }
    }
}

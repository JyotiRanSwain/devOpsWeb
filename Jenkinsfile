pipeline {
    agent {
    label 'linux'
    }
    
    tools {
        maven 'local_maven'
    }
stages{
        stage('Build'){
           steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deployments'){
            parallel{
                stage ("Deploy to Staging"){
                    steps {
                        echo 'Deploy successful'
                    }
                }
            }
        }
    }
}

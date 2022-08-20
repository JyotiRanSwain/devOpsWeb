pipeline {
    agent {
    label ('windows')
    }
    
    tools {
        maven 'local_maven'
    }
    
stages{
        stage('Build'){
            steps {
                sh 'mvnw clean package'
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

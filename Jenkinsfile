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
                echo 'build success'
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

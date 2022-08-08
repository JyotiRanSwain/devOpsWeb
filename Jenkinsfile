pipeline {
    agent any
    
    tools {
        maven 'local_maven'
    }
    parameters {
         string(name: 'staging_server', defaultValue: '43.205.118.109', description: 'Remote Staging Server')
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

    }
}

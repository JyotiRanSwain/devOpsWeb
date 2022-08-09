pipeline {
    agent any
    
    tools {
        maven 'local_maven'
    }
    parameters {
         string(name: 'staging_server', defaultValue: '13.233.141.101', description: 'Remote Staging Server')
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
                        deploy adapters: [tomcat7(credentialsId: '93fa21cf-5c24-47aa-bb94-77fa589bc10d', path: '', url: 'http://${params.staging_server}:8282/')], contextPath: null, war: '**/*.war'
                    }
                }
            }
        }
    }
}

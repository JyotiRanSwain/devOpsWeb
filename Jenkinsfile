pipeline {
    agent any
    
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
                        deploy adapters: [tomcat7(credentialsId: '93fa21cf-5c24-47aa-bb94-77fa589bc10d', path: '', url: 'http://13.233.141.101:8282/')], contextPath: null, war: '**/*.war'
                    }
                }
            }
        }
    }
}

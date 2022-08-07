pipeline {
    agent any
    
    tools {
        maven 'local_maven'
    }
    parameters {
         string(name: 'tomcat_stag', defaultValue: '3.111.144.29', description: 'Node1-Remote Staging Server')
             }
    triggers {
         pollSCM('* * * * *')
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
                    stage ('Deploy to Productio'){
                    steps {
                        sh "scp **/*.war jenkins@${params.tomcat_prod}:/usr/opt/tomcat/webapps/"
                }
            }
        }
    }
}

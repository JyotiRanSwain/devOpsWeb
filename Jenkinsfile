pipeline {
    agent any
    tools {
        maven 'local_maven'
    }
stages {
    stage('build') {
        steps{
            sh 'mvn clean package'
        }
        post {
            success {
                echo 'archiving the artifacts'
                archiveArtifacts artifacts: '**/target/*.war'
            }
        }
    }
    stage ('deploy'){
        steps{
            sshagent(['ubuntu-tomcat']) {
    sh "scp -v -o StrictHostKeyChecking=no **/*.war ubuntu@3.109.202.2:/opt/tomcat/webapps/"
}
        }
    }
}
}

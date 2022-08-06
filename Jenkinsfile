pipeline {
    agent any
    tools {
        maven 'local_maven'
          } 
    stages {
        stage('Build') { 
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
        stage('Test') { 
            steps {
                echo "Testing" 
            }
        }
        stage('Deploy') { 
            steps {
                echo "Deploing" 
            }
        }
    }
}

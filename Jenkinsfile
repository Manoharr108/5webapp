pipeline {
    agent any
    tools {
        maven 'maven'
        ansible 'ansible'  // <- Only if you configured it under Global Tools
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/manoharr108/5webapp.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }
        stage('Deploy') {
            steps {
                ansiblePlaybook(
                    playbook: 'ansible/deploy.yml',
                    inventory: 'ansible/hosts.ini',
                    colorized: true
                )
            }
        }
    }
}


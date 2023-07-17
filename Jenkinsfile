pipeline {
    agent {
        node {
            label 'maven'
        }
    }

    stages {
        stage('Clone-code') {
            steps {
                git branch: 'main', url: 'https://github.com/lambait01/devops-project-2-app.git'
            }
        }
    }
}
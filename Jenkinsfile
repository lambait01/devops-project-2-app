pipeline {
    agent {
        node {
            label 'maven'
        }
    }

environment {
    PATH = "/opt/apache-maven-3.9.3/bin:$PATH"
}

    stages {
        stage('Build') {
            steps {
                echo "----------- build just started ----------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "----------- build complted ----------"
            }
        }
    }
}
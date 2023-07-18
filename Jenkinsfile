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

        stage("test"){
            steps{
                echo "----------- unit test started ----------"
                sh 'mvn surefire-report:report'
                echo "----------- unit test Complted ----------"
            }
        }
    
        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'ttrend-sonarqube-scanner';   // the name we put when we add Tools on Jenkins
            }
            steps {
                withSonarQubeEnv('ttrend-sonarqube-server') { // Name entered in Jenkins / System / SonarQube servers | If you have configured more than one global server connection, you can specify its name
                sh "${scannerHome}/bin/sonar-scanner"
                } 
            }  
        }              

    }




}


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

        stage("Unit Test"){
            steps{
                echo "----------- unit test started ----------"
                sh 'mvn surefire-report:report'
                echo "----------- unit test Complted ----------"
            }
        }
    
        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool 'ttrend-sonarqube-scanner';   // the name we put when we add Tools on Jenkins
            }
            steps {
                withSonarQubeEnv('ttrend-sonarqube-server') { // Name entered in Jenkins / System / SonarQube servers | If you have configured more than one global server connection, you can specify its name
                sh "${scannerHome}/bin/sonar-scanner"
                } 
            }  
        }

        stage("Quality Gate"){
            steps {
                script {
                    timeout(time: 1, unit: 'HOURS') { // Just in case something goes wrong, pipeline will be killed after a timeout
                        def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
                        if (qg.status != 'OK') {
                            error "Pipeline aborted due to quality gate failure: ${qg.status}"
                        }
                    }
                }
            }
        }              

    }




}


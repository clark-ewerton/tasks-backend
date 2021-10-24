pipeline{
    agent any
    stages{
        stage('Build tasks backend'){
            steps{
                bat 'mvn test package -DskipTests=true'
            }
			}
 	stage('Unit Tests'){
            steps{
                bat 'mvn test'
            }
        }     
stage('Sonar Analysis'){
environment{
scannerHome = tool 'SONAR_SCANNER'
}
            steps{
withSonarQubeEnv('SONAR_LOCAL'){
                bat "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=deploy_back -Dsonar.host.url=http://localhost:9000 -Dsonar.login=6fcbbc6998a96a356027439d07eb31be394606c6 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn**,**/src/test/**,**/model/**,**/Application.java"
            }
        }      
}
}
}



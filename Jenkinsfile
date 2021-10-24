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
stage('Quality Gate'){
            steps{
sleep(5)
timeout(time: 1, unit: 'MINUTES'){
waitForQualityGate abortPipeline: true
}
            }
        }  
stage ('Deploy Backend') {

            steps {

                deploy adapters: [tomcat8(credentialsId: 'tomcat-login', path: '', url: 'http://localhost:8001/')], contextPath: 'tasks-backend', war: 'target/tasks-backend.war'

            }

        }
		  stage ('API Test') {

            steps {

                dir('api-test') {

                    git credentialsId: 'github_login', url: 'https://github.com/clark-ewerton/tasks-api-test'

                    bat 'mvn test'

                }

            }

        }
		
		   stage ('Deploy Frontend') {

            steps {

                dir('frontend') {

                    git credentialsId: 'github_login', url: 'https://github.com/clark-ewerton/tasks-frontend'

                    bat 'mvn clean package'

                    deploy adapters: [tomcat9(credentialsId: 'tomcat-login', path: '', url: 'http://localhost:8001/')], contextPath: 'tasks', war: 'target/tasks.war'

                }

            }

        }
		
		stage ('Functional Test') {

            steps {

                dir('functional-test') {

                    git credentialsId: 'github_login', url: 'https://github.com/clark-ewerton/tasks-functional-tests'

                    sh 'mvn test'

                }

            }

        

        }
}



pipeline{
    agent any
    stages{
        stage('Build tasks backend'){
            steps{
                bat 'mvn test package -DskipTests=true'
            }
 stage('Unit Tests'){
            steps{
                bat 'mvn test'
            }
        }
        }
}
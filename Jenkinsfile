pipeline{
    agent any
    stages{
        stage('Inicio'){
            steps{
                bat 'echo Inicio'
            }
        }
         stage('Meio'){
            steps{
                bat 'echo meio'
                 bat 'echo meio de novo'
            }
        }
         stage('Fim'){
            steps{
                sleep(5)
                bat 'echo Fim'
            }
        }
    }
}
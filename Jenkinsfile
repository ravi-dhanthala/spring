pipeline {
    agent any

    stages {
        stage('clone') {
            steps {
               git branch: 'feature/2025.06.22', url: 'https://github.com/ravi-dhanthala/spring.git'
            }
        }
        stage('build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('test'){
            steps{
                sh 'mvn test'
            }
        }
        stage('test results'){
            steps{
                junit allowEmptyResults: true, keepProperties: true, keepTestNames: true, stdioRetention: 'ALL', testResults: 'target/surefire-reports/*.xml'
            }
        }
        stage('artifacts'){
            steps{
                archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
            }
        }
    }
    post{
        success{
            echo "Everything succeeded!"
        }
        failure{
            echo "something went wrong"
        }
    }
}

pipeline {
    agent any

    stages {
        stage('Build'){
            steps {
                git 'https://github.com/JerryGB7/pipeline-practice.git'
                sh 'docker build -t jerrygb7/pipeline-practice:latest .'
                sh 'python3 -m pip install -r requirements.txt'
            }
        }
        stage ('Test'){
            steps{
                sh 'python3 -m pytest app-test.py'
            }
        }
        stage('Deploy'){
            steps{
                withCredentials([string(credentialsId: 'passwd', variable: 'dockerpwd')]){
                    sh 'docker login -u jerrygb7 -p ${dockerpwd}'
                }
                sh 'docker push jerrygb7/pipeline-practice:latest'
            }
        }
        stage('Run'){
            steps{
                sh 'python3 -m flask run --host="0.0.0.0" &'
            }
        }
    }
}
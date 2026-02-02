pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/23mh1a0553/charitize.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                docker stop webapp || true
                docker rm webapp || true
                '''
            }
        }

        stage('Remove Old Image') {
            steps {
                sh '''
                docker rmi demo || true
                '''
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t amazon .'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh 'docker run -d -p 6060:8080 --name azure amazon'
            }
        }
    }
}

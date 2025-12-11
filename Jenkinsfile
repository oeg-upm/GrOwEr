pipeline {
    agent { label 'GrOwEr' }

    environment {
        DOCKERHUB = credentials('oeg-dockerhub')

        IMAGE = 'jarueda/oeg-grower'
        TAG   = 'latest'
    }

    stages {
        stage('Build') {
            steps {
                sh "docker build -t ${IMAGE}:${TAG} ."
            }
        }

        stage('Login') {
            steps {
                sh "echo ${DOCKERHUB_PSW} | docker login -u ${DOCKERHUB_USR} --password-stdin"
            }
        }

        stage('Push') {
            steps {
                sh "docker push ${IMAGE}:${TAG}"
            }
        }
    }

    post {
        always {
            sh 'docker logout || true'
            cleanWs()
        }
    }
}

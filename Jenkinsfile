pipeline{
    agent { label 'GrOwEr'}
}
environment{
    DOCKERHUB_CREDENTIALS = credentials('oeg-dockerhub')
}
stages{
    stage('Build'){
        steps{
            sh 'docker build -t jarueda/oeg-grower:latest .'
        }
    }
    stage('Login'){
        steps{
            sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        }
    }
    stage('Push'){
        steps{
            sh 'docker push jarueda/oeg-grower:latest'
        }
    }
}
post{
    always{
        sh 'docker logout'
    }
}
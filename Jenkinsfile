pipeline {

    agent {
        label 'builder'
    }

    stages {
        stage ('Get code and build artifact') {
            steps {
                sh 'docker build . -t myapp1:$BUILD_NUMBER'
            }
        }
        stage('Push artifact)') {
            steps {
                sh 'docker tag myapp1:$BUILD_NUMBER 81.26.183.248:8082/myapp1:$BUILD_NUMBER'
                withCredentials([usernamePassword(credentialsId: '3a4a8403-586d-4657-afbe-85f8684e491d', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh "docker login -u $DOCKER_USER -p $DOCKER_PASS 81.26.183.248:8082"
                    sh 'docker push my-app:$BUILD_NUMBER'
                }
            }
        }
    }
}    
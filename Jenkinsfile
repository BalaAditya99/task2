pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "balaaditya99/myapp"
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Replace this with actual test commands
                sh 'echo "Tests passed!"'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                withCredentials([string(credentialsId: 'balaaditya99', variable: 'DOCKER_PASS')]) {
                    sh '''
                    echo $DOCKER_PASS | docker login -u yourdockerhubusername --password-stdin
                    docker push $DOCKER_IMAGE
                    '''
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'docker system prune -f'
        }
    }
}
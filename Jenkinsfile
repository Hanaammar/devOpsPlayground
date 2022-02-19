pipeline {
    agent any
    environment {
    DockerHost = '352708296901.dkr.ecr.us-east-1.amazonaws.com'
    Image = 'eliasrepo:${BRANCH_NAME}_{BUILD_NUMBER}'
    }

    stages {
        stage('Build') {
        when {anyOf { branch "master"; branch "dev"}}
            steps {
                echo 'Building..'
                sh '''
                cd simple_webserver
                echo ${BRANCH_NAME}
                aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin ${DockerHost}
                docker build -t eliasrepo .
                docker tag ${Image} ${DockerHost}/${Image}
                docker push ${DockerHost}/${Image}

                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
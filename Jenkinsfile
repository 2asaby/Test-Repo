pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the Java application'
                sh './mvnw clean package'
            }
        }
        stage ('test') {
            steps {
                echo 'Testing the Java application'
                sh './mvnw test'
            }
        }
        stage ('Docker Build and Push') {
            steps {
                script {
                    echo 'Building and pushing to Docker hub'
                    docker.build("2asaby/devops:jenkins-test")

                    docker.withRegistry('https://index.docker.io/v1/', 'my-docker-hub') {
                        docker.image("2asaby/devops:jenkins-test").push()
                    }
                }
            }        
        }
    }
}

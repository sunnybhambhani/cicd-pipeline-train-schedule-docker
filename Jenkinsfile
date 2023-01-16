pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        stage('Docker Build') {
            when {
                branch 'master'
            }
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker') {
                        sh "docker image build -t sunnybhambhani:latest ."
                        sh "docker image tag sunnybhambhani:latest sunnybhambhani:${env.BUILD_NUMBER}"

                        sh "docker push sunnybhambhani/node:${env.BUILD_NUMBER}"
                        sh "docker push sunnybhambhani/node:latest'

                        echo "Image built and pushed to repository"
                    }
                }
            }
        }
    }
}

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
      	    sh "docker build -t sunnybhambhani/node:${env.BUILD_NUMBER} ."
            sh "docker push sunnybhambhani/node:${env.BUILD_NUMBER}"
            }
        }
    }
}

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
        stage('BuildDockerImage') {
            when {
                branch 'master'
            }
            steps {
                sh 'docker build -t lu23/trainschedule .'
                sh 'docker images'
            }
        }
        stage('PushDockerImage') {
            when {
                branch 'master'
            }
            steps {
                echo 'Pushing images to dockerHub'
            }
        }
        stage('DeployToProduction') {
            when {
                branch 'master'
            }
            steps {
                echo 'Deploying to production'
            }
        }
    }
}

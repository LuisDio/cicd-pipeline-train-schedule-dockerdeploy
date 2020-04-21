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
        stage('Build docker image') {
            steps {
                sh 'docker built -t lu23/trainSchedule .'
                sh 'docker images'
            }
        }
    }
}

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
        stage('Build Docker image') {
            when {
                branch 'master'
            }
            script {
                steps {
                    image = docker.build("lu23/train-schedule")

                    image.inside {
                        sh 'echo $(curl localhost:8080)'
                    }
                }
            }
        }
        stage('Push Docker Image') {
            when {
                branch 'master'
            }
            script {    
                docker.withRegistry('https://registry.hub.docker.com', 'DockerHub') {
                    image.push("${env.BUILD_NUMBER}")
                    image.push("latest")
                }
            }
            
        }
        stage('Deploy to production') {
            when {
                branch 'master'
            }

            steps {
                input 'Deploy to production'
                milestone(1)
            }
        }
    }
}

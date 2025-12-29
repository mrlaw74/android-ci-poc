pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/mrlaw74/android-ci-poc.git'
            }
        }

        stage('Start Emulator') {
            steps {
                sh '''
                docker start android-emulator || true
                sleep 40
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                adb connect android-emulator:5554
                cd app
                ./gradlew connectedAndroidTest
                '''
            }
        }
    }

    post {
        always {
            sh 'docker stop android-emulator || true'
        }
    }
}

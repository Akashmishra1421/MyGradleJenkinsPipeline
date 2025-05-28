pipeline {
    agent any
    tools {
        gradle 'Gradle'          // Your Jenkins Gradle tool name
        jdk 'Java Development Kit'  // Your Jenkins JDK tool name
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Akashmishra1421/MyGradleJenkinsPipeline.git'
            }
        }
        stage('Build') {
            steps {
                sh 'gradle build'
            }
        }
        stage('Test') {
            steps {
                script {
                    def hasTestTask = sh(script: "gradle tasks --all | grep 'test -'", returnStatus: true) == 0
                    if (hasTestTask) {
                        sh 'gradle test'
                    } else {
                        echo "Skipping tests: 'test' task not found."
                    }
                }
            }
        }
        stage('Run Application') {
            steps {
                script {
                    def hasRunTask = sh(script: "gradle tasks --all | grep 'run -'", returnStatus: true) == 0
                    if (hasRunTask) {
                        sh 'gradle run'
                    } else {
                        echo "Skipping run: 'run' task not found."
                    }
                }
            }
        }
    }
    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}


pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
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
     post {
        always {
        mail to: 'jsr2089@gmail.com',
             subject: "Status: ${currentBuild.fullDisplayName}",
             body: "Test ${env.BUILD_URL}"
        }
    }

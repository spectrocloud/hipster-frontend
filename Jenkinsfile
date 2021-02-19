pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building 3..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
    post {
        success {
            script {
                if (env.CHANGE_ID) {
                    pullRequest.addLabel('Build Success - URL http://${hipster_url}')
                }
            }
        }
    }
}

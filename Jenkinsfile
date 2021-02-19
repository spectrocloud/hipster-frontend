pipeline {
    agent any

    environment {
        imagename = "gcr.io/spectro-palette-dev/demo"
        registryCredential = 'Docker'
        dockerImage = ''
    }


    stages {
        stage('Build') {
            steps {
                echo 'Building 3..'
                script {
                    dockerImage = docker.build hipster
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                docker.withRegistry( '', registryCredential ) {
                    dockerImage.push("$BUILD_NUMBER")
                    dockerImage.push('latest')
                }
            }
        }
        stage('Remove Unused docker image') {
            steps{
                sh "docker rmi $imagename:$BUILD_NUMBER"
                sh "docker rmi $imagename:latest"
             }
        }
    }
    post {
        success {
            script {
                echo "Build Success - URL http://${hipster_url}"
                if (env.CHANGE_ID) {
                    pullRequest.addLabel('Build Success - URL http://${hipster_url}')
                }
            }
        }
    }
}

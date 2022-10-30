

pipeline {
    agent any
    environment {
        dockerhub=credentials('Docker_Hub')
    }
    stages {
        stage('Build BackHouse') {
            steps {
               sh "docker login -u $dockerhub_USR -p $dockerhub_PSW"
               sh "docker build -t back_house:v1 ."
            }
            // post {
            //     success {
            //         slackSend (channel: 'jenkins-multibranch', color: '#00FF00', message: "BUILD STAGE SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'[${env.BRANCH_NAME}]")

            //     }
            //     failure {
            //         slackSend (channel: 'jenkins-multibranch', color: '#FF0000', message: "BUILD STAGE FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' [${env.BRANCH_NAME}]")
            //     }
            // }
        }
        stage('Push BackHouse') {
            steps {
                sh 'docker tag back_house:v1 mohamedalaaelsafy/app:v1'
                sh 'docker push mohamedalaaelsafy/app:v1'
            }
        
            // post {
            //     success {
            //         slackSend (channel: 'jenkins-multibranch', color: '#00FF00', message: "BUILD STAGE SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' [${env.BRANCH_NAME}]")

            //     }
            //     failure {
            //         slackSend (channel: 'jenkins-multibranch', color: '#FF0000', message: "BUILD STAGE FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'[${env.BRANCH_NAME}]")
            //     }
            // }
        }

        stage('Deploy BackHouse') {
            steps {
                sh 'docker tag back_house:v1 mohamedalaaelsafy/app:v1'
                sh 'docker push mohamedalaaelsafy/app:v1'
            }
        
            post {
                success {
                    slackSend (channel: 'jenkins-multibranch', color: '#00FF00', message: "BUILD STAGE SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' [${env.BRANCH_NAME}]")

                }
                failure {
                    slackSend (channel: 'jenkins-multibranch', color: '#FF0000', message: "BUILD STAGE FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'[${env.BRANCH_NAME}]")
                }
            }
        }
    }

    post {
        success {
            echo 'This will run only if successful'
        }
    }
}

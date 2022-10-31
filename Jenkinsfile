

pipeline {
    agent { label 'jenkins-agent' }
    environment {
        dockerhub=credentials('Docker_Hub')
    }
    stages {
        stage('Build & Deploy') {
     steps {
                script {
                    if (env.BRANCH_NAME == 'master') {
                        sh "docker login -u $dockerhub_USR -p $dockerhub_PSW"
                        sh "docker build -t back_house:v1 ."
                        sh 'docker tag back_house:v1 mohamedalaaelsafy/app:v1'
                        sh 'docker push mohamedalaaelsafy/app:v1'
                } else if (env.BRANCH_NAME == 'stage' || env.BRANCH_NAME == 'dev' || env.BRANCH_NAME == 'test') {
                withCredentials([file(credentialsId: 'config', variable: 'cfg')]){
                        sh 'kubectl apply -f Deployment/service.yaml'
                        sh 'kubectl apply -f Deployment/deploy.yaml'
                 }
                } else {
                        sh 'echo Not master nor stage'
                    }
                }
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
        // stage('Push BackHouse') {
        //     steps {
        //         sh 'docker tag back_house:v1 mohamedalaaelsafy/app:v1'
        //         sh 'docker push mohamedalaaelsafy/app:v1'
        //     }
        
            // post {
            //     success {
            //         slackSend (channel: 'jenkins-multibranch', color: '#00FF00', message: "BUILD STAGE SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' [${env.BRANCH_NAME}]")

            //     }
            //     failure {
            //         slackSend (channel: 'jenkins-multibranch', color: '#FF0000', message: "BUILD STAGE FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'[${env.BRANCH_NAME}]")
            //     }
            // }
        // }

        // stage('Deploy BackHouse') {
        //     steps {
        //         sh 'kubectl apply -f Deployment/service.yaml --validate=false'
        //         sh 'kubectl apply -f Deployment/Deploy.yaml --validate=false'
        //     }
        
            // post {
            //     success {
            //         slackSend (channel: 'jenkins-multibranch', color: '#00FF00', message: "BUILD STAGE SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' [${env.BRANCH_NAME}]")

            //     }
            //     failure {
            //         slackSend (channel: 'jenkins-multibranch', color: '#FF0000', message: "BUILD STAGE FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'[${env.BRANCH_NAME}]")
            //     }
            // }
        // }
    }

    post {
        success {
            echo 'This will run only if successful'
        }
    }
}

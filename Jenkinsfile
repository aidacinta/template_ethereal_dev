pipeline {
    agent any
    // agent { dockerfile true }
    environment {
        DOCKER_IMAGE = 'test3'
        CONTAINER_NAME = 'jhgfd'
        PORT_MAPPING = '8082:80'  // Adjust the port mapping as needed
    }

    stages {
        // stage('Checkout') {
        //     steps {
        //         // Clean workspace before checkout
        //         deleteDir()
        //         // Checkout the HTML source code from GitHub
        //         git url: 'https://github.com/andrinahaura/project1.git'
        //     }
        // }
            stage('Checkout') {
                steps {
                    deleteDir()
                    checkout([$class: 'GitSCM', branches: [[name: 'main']], userRemoteConfigs: [[url: 'https://github.com/ilham275/template_ethereal.git']]])
                    // docker.build("${DOCKER_IMAGE}",'-f Dockerfile .')

                }
            }

        stage('Build Docker Image') {
            steps {
                script {
                    // dir('testdeploy') {
                    //   sh 'ls -l'

                        // Build Docker image dengan konten HTML
                        // sh 'docker build -t test3 -f Dockerfile .'
                        docker.build("${DOCKER_IMAGE}",'-f Dockerfile .')
                        // sh 'docker build -t test3 -f Dockerfile .'
                    // }
                    // // Build Docker image with the HTML content
                    // docker.build("${DOCKER_IMAGE}", '-f Dockerfile .')
                }
            }
        }


    
        stage('Run Docker Container') {
            steps {
                script {
                    // Run Docker container based on the built image
                    docker.image("${DOCKER_IMAGE}").run("-p ${PORT_MAPPING} --name ${CONTAINER_NAME}")
                }
            }
        }
    }

      post {
        always {
            script {
                // Stop and remove the Docker container after execution
                docker.container(CONTAINER_NAME).stop()
                docker.container(CONTAINER_NAME).remove(force: true)
            }
        }
    }
}
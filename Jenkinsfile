pipeline {
    agent any
    environment {
        registry = "c1l2o3u4d5/todoappl"
        registryCredential = 'docker-hub-credentials'
        dockerImage = '' 
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building the ToDo application on Docker'
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Push') {
            steps {
                echo 'Pushing the ToDo application Docker image'
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application on Docker'
                     
                script {
                    def deployedContainer = docker.container('todoappl').run('-p 3000:3000')
            // Additional configuration or operations if needed
                    deployedContainer.stop()
                        // Additional steps or configurations if needed inside the running container
                    }
                }
                
            }
        }
    }
}

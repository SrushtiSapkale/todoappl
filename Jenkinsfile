pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the ToDo application on Docker'
                script {
                    def env = docker.build 'todoappl'
                }
            }
        }
        stage('Push') {
            steps {
                echo 'Pushing the ToDo application Docker image'
                script {
                    env.push()
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application on Docker'
               
                docker.run("-p 3000:3000 -dp --name todo-container ${env.id}")
                    // or use sh 'docker run -p 3000:3000 -d todoappl'
                
            }
        }
    }
}

pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/your-repo/springboot-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t springboot-app .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker stop springboot-app || true'
                sh 'docker rm springboot-app || true'
                sh 'docker run -d -p 8080:8080 --name springboot-app -e spring.datasource.url=jdbc:mysql://<EC2_PUBLIC_IP>:3306/springbootdb springboot-app'
            }
        }
    }
}

pipeline {
    agent any

    environment {
        DOCKERHUB = credentials('dockerhub')
        IMAGE_NAME = "kalyan0530/my_python_jenkins_pipeline"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/YOUR_GITHUB_USERNAME/kalyan-python-jenkins-project.git'
            }
        }

        stage('Install Python Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Python Script') {
            steps {
                sh 'python app.py'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                sh 'echo $DOCKERHUB_PSW | docker login -u $DOCKERHUB_USR --password-stdin'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $IMAGE_NAME'
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
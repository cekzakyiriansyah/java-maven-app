pipeline {
    agent any

    tools {
        // Sesuaikan dengan nama Maven yang terdaftar di Jenkins
        maven 'maven-app'
    }

    stages {
        stage('Build jar') {
            steps {
                echo "📦 Building the JAR file..."
                sh 'mvn package'
            }
        }

        stage('Build Image') {
            steps {
                script {
                    echo "🐳 Building the Docker image..."
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh 'docker build -t zaky21/demo-app:imp-2.0 .'
                        sh "echo \$PASS | docker login -u \$USER --password-stdin"
                        sh 'docker push zaky21/demo-app:imp-2.0'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo "🚀 Deploying the application..."
                    // Tambahkan perintah deploy jika ada (misal kubectl apply, docker run, dll)
                }
            }
        }
    }
}

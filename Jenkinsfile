@Library("Shared") _

pipeline {
    agent { label "v1" }

    environment {
        DOCKER_BUILDKIT = "1"
        DOCKERHUB = credentials('dockerHubCred')
    }

    stages {

        stage("Hello") {
            steps {
                script {
                    hello()
                }
            }
        }

        stage("Checkout Code") {
            steps {
                echo "Cloning repository..."
                clonning("https://github.com/gehlotnikhil/django-notes-app.git","main")
                echo "Code cloned successfully!"
            }
        }

        stage("Build Docker Images") {
            steps {
                echo "Building application and nginx Docker images with caching..."
                dockerBuild("$DOCKERHUB_USR","notes-app","latest",".")
                dockerBuild("$DOCKERHUB_USR","notes-app-nginx","latest","./nginx")
                echo "Docker images built successfully!"
            }
        }

        stage("Push to DockerHub") {
            steps {
                echo "Pushing images to DockerHub..."
                dockerPush2("${DOCKERHUB_USR}","${DOCKERHUB_PSW}","notes-app","latest")
                dockerPush2("${DOCKERHUB_USR}","${DOCKERHUB_PSW}","notes-app-nginx","latest")
                echo "Pushed images successfully!"
            }
        }

        stage("Deploy") {
            steps {
                echo "Deploying using docker-compose..."
                dockerCompose()
                echo "Deployment complete!"
            }
        }
    }
}

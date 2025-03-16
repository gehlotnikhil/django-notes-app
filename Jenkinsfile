@Library("Shared") _
pipeline {
    agent any
    stages {
        stage("Code") {
            steps {
                echo "Cloning the repository..."
                sh "whoami"
                clonning("https://github.com/gehlotnikhil/django-notes-app.git","main")
                echo "Code Clone Successful"
            }
        }

       stage("Build") {
            steps {
                echo "Building the Docker image...."
                dockerBuild("notes-app","latest","gehlotnikhil38")
                echo "Build Successful"
            }
        }

        stage("Push to DockerHub") {
            steps {
             echo "Pushing to DockerHub process Started"
             dockerPush("notes-app","latest","gehlotnikhil38")
                echo "Image pushed successfully!"
            }
        }
    }
}

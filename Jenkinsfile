node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    // Only build and push if we're on the 'dev' branch
    if (env.BRANCH_NAME == 'dev') {
        stage('Build image') {
            app = docker.build("itonkdong/kiii-homework-4")
        }

        stage('Push image') {
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
            }
        }
    } else {
        stage('Skip Docker') {
            echo "Skipping Docker build and push because branch is '${env.BRANCH_NAME}'"
        }
    }
}

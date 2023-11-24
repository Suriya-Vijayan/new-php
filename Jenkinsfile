node {
    stage('Code Checkout') {
        echo 'Code checkout from the git repo'
        git 'https://github.com/Suriya-Vijayan/new-php'
    }

    stage('Building the application') {
        echo 'Moving inside the directory and then building the application'
        sh 'docker build -t suriyavijayan/php-web-app .'
    }

    stage('Pushing docker image') {
        echo 'Pushing docker image to Docker Hub'
        def dockerHubCredentials = 'docker-hub-credentials'
        withCredentials([usernamePassword(credentialsId: dockerHubCredentials, usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
            sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
            sh 'docker push suriyavijayan/php-web-app:latest'
        }
    }
    
    stage ('Application Deployment'){
        echo 'Deploying the application in the server'
        sh 'docker run -d -p 8081:80 suriyavijayan/php-web-app:latest'
    } 
}

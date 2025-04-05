pipeline {
    agent any
 environment {
        SONARQUBE_SERVER = 'sonarqubeserver' // Replace with your SonarQube server name configured in Jenkins
        NODE_HOME = "${tool 'NodeJsTool'}" // Replace 'NodeJS' with the NodeJS tool name configured in Jenkins
    }
    stages {
      stage('Clean Workspace') {
            steps {
                cleanWs() // This function cleans the workspace
                echo 'Workspace cleaned successfully!'
            }
        }
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/gothinkster/angular-realworld-example-app.git' // Replace with your repository URL and branch
            }
        }
       stage('Install Dependencies') {
            steps {
                script {
                    env.PATH = "${NODE_HOME}\\bin;${env.PATH}" // Use double backslashes for Windows paths
                    bat 'npm install core-js@latest'
                    bat 'npm cache clean --force'
                    bat 'npm install --legacy-peer-deps'
                    bat 'ng build'
                }
                            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                // Add your build commands here, e.g., `sh 'mvn clean install'`
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Add your test commands here, e.g., `sh 'mvn test'`
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
                // Add your deployment commands here
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}

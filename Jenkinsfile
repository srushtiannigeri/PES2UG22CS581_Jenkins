pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/srushtiannigeri/PES2UG22CS581_Jenkins.git',
                        credentialsId: 'github-credentials-id'
                    ]]
                ])
            }
        }
        
        stage('Build') {
            steps {
                script {
                    sh 'g++ -o PES2UG22CS581-1 hello.cpp'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh '''
                    chmod +x PES2UG22CS581-1
                    ./PES2UG22CS581-1
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh 'git config --global user.name "Srushti Annigeri"'
                    sh 'git config --global user.email "annigerisrushti@gmail.com"'
                    sh 'git checkout main'
                    sh 'git add -A'
                    sh 'git commit -m "Added hello.cpp file" || echo "No changes to commit"'
                    sh 'git push origin main'
                }
            }
        }
    }

    post {
        success {
            echo "Build and deployment successful!"
        }
        failure {
            echo "Pipeline failed"
        }
    }
}

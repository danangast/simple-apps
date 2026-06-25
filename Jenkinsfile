pipeline {
    agent {label 'dev1-danang'}
    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/danangast/simple-apps.git'
            }
        }
        stage('Build') {
            steps {
                sh '''cd apps
                npm install'''
            }
        }
        stage('Testing') {
            steps {
                sh '''cd apps
                npm test
                npm run test:coverage'''
            }
        }
        stage('Code Review') {
            steps {
                sh '''
                cd apps
            sonar-scanner \
            -Dsonar.projectKey=project2-simple-apps \
            -Dsonar.sources=. \
            -Dsonar.host.url=http://172.23.4.116:9000 \
            -Dsonar.token=sqp_e3e8e5e591fdd8d0444c2f7189978198f5b830ad
            '''
            }
        }
        stage('Deploy compose') {
            steps {
                sh '''
                docker compose build
                docker compose up -d
                '''
            }
        }
    }
}
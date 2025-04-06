pipeline {
    agent any
    
    triggers {
        pollSCM('*/1 * * * *')
    }
    
    stages {
        stage('install-pip-deps') {
            steps {
                echo 'Installing all required dependencies...'
            }
        }

        stage('deploy-to-dev') {
            steps {
                echo 'Deploying to development environment...'
            }
        }

        stage('tests-on-dev') {
            steps {
                echo 'Running tests on development environment...'
            }
        }

        stage('deploy-to-staging') {
            steps {
                echo 'Deploying to staging environment...'
            }
        }

        stage('tests-on-staging') {
            steps {
                echo 'Running tests on staging environment...'
            }
        }

        stage('deploy-to-preprod') {
            steps {
                echo 'Deploying to pre-production environment...'
            }
        }

        stage('tests-on-preprod') {
            steps {
                echo 'Running tests on pre-production environment... '
            }
        }

        stage('deploy-to-prod') {
            steps {
                echo 'Deploying to production environment...'
            }
        }

        stage('tests-on-prod') {
            steps {
                echo 'Running tests on production environment...'
            }
        }
    }
}
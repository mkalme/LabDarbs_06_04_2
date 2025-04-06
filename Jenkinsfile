pipeline {
    agent any
    
    triggers {
        pollSCM('*/1 * * * *')
    }
    
    stages {
        stage('install-pip-deps') {
            steps {
                build()
            }
        }

        stage('deploy-to-dev') {
            steps {
                deploy("development")
            }
        }

        stage('tests-on-dev') {
            steps {
                test("development")
            }
        }

        stage('deploy-to-staging') {
            steps {
                deploy("staging")
            }
        }

        stage('tests-on-staging') {
            steps {
                test("staging")
            }
        }

        stage('deploy-to-preprod') {
            steps {
                deploy("pre-production")
            }
        }

        stage('tests-on-preprod') {
            steps {
                test("pre-production")
            }
        }

        stage('deploy-to-prod') {
            steps {
                deploy("production")
            }
        }

        stage('tests-on-prod') {
            steps {
                test("production")
            }
        }
    }
}

def build(){
    echo 'Installing all required dependencies...'

    bat 'if exist python-greetings rmdir /s /q python-greetings'
    bat 'git clone https://github.com/mtararujs/python-greetings'
    bat 'cd python-greetings'
    bat 'pip install -r requirements.txt'
}

def deploy(String environment){
    echo "Deploying to production ${environment}..."
}

def test(String environment){
    echo "Running tests on production ${environment}..."
}
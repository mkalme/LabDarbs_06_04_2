pipeline {
    agent any
    
    triggers {
        pollSCM('*/1 * * * *')
    }
    
    stages {
        stage('install-pip-deps') {
            steps {
                buildApp()
            }
        }

        stage('deploy-to-dev') {
            steps {
                deploy("dev", 7001, "development")
            }
        }

        stage('tests-on-dev') {
            steps {
                test("dev", "greetings", "development")
            }
        }

        stage('deploy-to-staging') {
            steps {
                deploy("stg", 7002, "staging")
            }
        }

        stage('tests-on-staging') {
            steps {
                test("stg", "greetings", "staging")
            }
        }

        stage('deploy-to-preprod') {
            steps {
                deploy("preprod", 7003, "pre-production")
            }
        }

        stage('tests-on-preprod') {
            steps {
                test("preprod", "greetings", "pre-production")
            }
        }

        stage('deploy-to-prod') {
            steps {
                deploy("prod", 7004, "production")
            }
        }

        stage('tests-on-prod') {
            steps {
                test("prd", "greetings", "production")
            }
        }
    }
}

def buildApp(){
    echo 'Installing all required dependencies...'

    sh '''
        if [ -d "python-greetings" ]; then 
            rm -rf python-greetings
        fi
        git clone https://github.com/mtararujs/python-greetings
        cd python-greetings
        pip install -r requirements.txt --break-system-packages
    '''
}

def deploy(String environment, int port, String type){
    echo "Deploying to production ${type}..."

    sh """
        pm2 delete greetings-app-${environment} || true
        cd python-greetings
        pm2 start app.py --name greetings-app-${environment} -- --port ${port}
    """
}

def test(String environment, String testSuite, String type){
    echo "Running tests on production ${type}.. ."

    sh """
        if [ -d "course-js-api-framework" ]; then 
            rm -rf course-js-api-framework
        fi
        git clone https://github.com/mtararujs/course-js-api-framework
        cd course-js-api-framework
        npm run ${testSuite} ${testSuite}_${environment}
    """
}
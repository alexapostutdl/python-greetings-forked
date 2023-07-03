pipeline {
    agent any
    stages {
        stage('build-docker-image') {
            steps {
                build_docker_image()
            }
        }
        stage('deploy-dev') {
            steps {
                deploy("dev")
            }
        }
        stage('api-tests-dev') {
            steps {
                run_api_tests("DEV")
            }
        }
        stage('deploy-stg') {
            steps {
                deploy("stg")
            }
        }
        stage('api-tests-stg') {
            steps {
                run_api_tests("STG")
            }
        }
        stage('deploy-prodd') {
            steps {
                deploy("prod")
            }
        }
        stage('api-tests-prod') {
            steps {
                run_api_tests("PROD")
            }
        }
    }
}

def build_docker_image(){
    echo "Building docker image.."
    sh "docker build --no-cache -t alexapostu/python-greetings:latest ."

    echo "Pushing docker image to docker registry.."
    sh "docker push alexapostu/python-greetings"
}

def deploy(String environment){
    echo "Deployment triggered on ${environment} environment.."
    sh "docker-compose stop python-greetings-${environment}"
    sh "docker-compose rm python-greetings-${environment}"
    sh "docker-compose up -d python-greetings-${environment}"
}

def run_api_tests(String environment){
    echo "API tests triggered on ${environment} environment.."
    sh "ls"
}

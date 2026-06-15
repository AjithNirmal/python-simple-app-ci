pipeline {
    agent any

    options {
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

    parameters {
        gitParameter type: 'PT_BRANCH',
                      name: 'A_BRANCH',
                      branchFilter: 'origin/(.*)',
                      defaultValue: 'master',
                      description: 'Choose a branch to checkout',
                      selectedValue: 'DEFAULT',
                      sortMode: 'DESCENDING_SMART'
    }

    environment {
        repo_url = "https://github.com/AjithNirmal/python-simple-app-ci.git"
    }

    stages {
        stage('Cleanup the WorkSapce') {
            steps {
                cleanWs()
            }
        }

        stage('Checkout') {
            steps {
                git branch: "${params.A_BRANCH}", url: "${env.repo_url}"
            }
        }

        stage('Creating virtual venv') {
            steps {
                sh """
                python3 -m venv .venv
                """
            }
        }

        stage('Installing the dependencies') {
            steps {
                sh """
                .venv/bin/pip install --no-cache-dir -r requirements.txt
                """
            }
        }
        stage('Running the TestCases'){
            steps{
                script{
                    if (params.RUN_TESTS == 'YES' ) {
                        echo "Running "
                    }
                    else {
                        echo "Not Running unit test cases kiddo "
                    }
                }
            }
        }
    }
    post {
       always {
                cleanWs()
            }
            success {
                echo "A lot of learning kiddo"
            }
            failure {
                echo "Failed kiddo"
            }
        }
}

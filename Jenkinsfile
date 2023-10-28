pipeline {
    agent any

    options {
        buildDiscarder(logRotator(numToKeepStr: '2', artifactNumToKeepStr: '2'))
    }

    stages {
        
        stage('Checkout external proj') {
        steps {
            git branch: 'master',
                url: 'git@https://github.com/pierresendorek/spring-petclinic-jenkins-pipeline.git'
           
        }
    }

        stage('Install the required packages') {
            steps {
                script {
                    sh 'pip install -r requirements.txt'
                }
            }
        }

        stage('Install the application') {
            steps {
                script {
                    sh 'pip install .'
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                        sh 'pytest .'
                }
            }
        }

        stage('Deployment of the application on Docker container') {
            steps {
                script {
                    sh 'docker build . --name spring-petclinic'
                }
            }
        }
    }
}

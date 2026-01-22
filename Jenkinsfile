pipeline {
    agent any

    parameters {
        string(name: 'BRANCH', defaultValue: 'master', description: 'Git branch name')
        choice(name: 'ENV', choices: ['dev', 'qa', 'prod'], description: 'Target environment')
    }

    stages {

        stage('Checkout') {
            steps {
                echo "Checking out source code..."
                git branch: params.BRANCH,
                    url: 'https://github.com/betawins/spring3-mvc-maven-xml-hello-world-1.git'
            }
        }

        stage('Parallel Build & Info') {
            parallel {

                stage('Maven Build') {
                    steps {
                        echo "Building project for ${params.ENV}"
                        sh 'mvn clean package'
                    }
                }

                stage('Environment Info') {
                    steps {
                        echo "Environment Selected: ${params.ENV}"
                        sh 'uname -a'
                    }
                }

                stage('Workspace Info') {
                    steps {
                        sh 'ls -l'
                    }
                }
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.war,target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "Gayas 546 Jenkins Parallel & Parameterized Pipeline SUCCESS"
        }
        failure {
            echo " Pipeline FAILED"
        }
    }
}

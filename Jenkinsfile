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
                        // Fix: Force Java 8 compilation
                        sh 'mvn clean package -Dmaven.compiler.source=1.8 -Dmaven.compiler.target=1.8'
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
                        echo "Workspace files:"
                        sh 'ls -l'
                    }
                }
            }
        }

        stage('Archive Artifact') {
            steps {
                echo "Archiving artifacts..."
                archiveArtifacts artifacts: 'target/*.war,target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "Gayas 546 Jenkins Parallel & Parameterized Pipeline SUCCESS"
        }
        failure {
            echo "Pipeline FAILED"
        }
    }
}

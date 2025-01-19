
pipeline {
    agent any
    tools {
        jdk 'OpenJDK 17'
        maven 'maven'
    }
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }
    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/AmaniOueslati/EbankApp.git'
            }
        }
        stage('Compile') {
            steps {
                sh "mvn clean compile -DskipTests"
            }
        }
        stage('SonarQube Analysis') {
            steps {
                sh """
                $SCANNER_HOME/bin/sonar-scanner \
                -Dsonar.host.url=http://localhost:9000 \
                -Dsonar.login=sqa_2caef61b71ccff4d81335405c989734b33d0a21d \
                -Dsonar.projectKey=test1 \
                -Dsonar.projectName=test1 \
                -Dsonar.sources=. \
                -Dsonar.java.binaries=target/classes
                """
            }
        }



/CD/

 stage('DEPENDENCY-CHECK') {
            steps {
                dependencyCheck additionalArguments: '--format HTML', odcInstallation: 'DP'
            }
        }
        stage('Archive Report') {
            steps {
                archiveArtifacts artifacts: '**/dependency-check-report.html', allowEmptyArchive: true
            }
        }
        stage('BUILD-APP') {
            steps {
                sh "mvn clean install -DskipTests"
            }
        }
        stage('BUILD & Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: '005a0d68-d68f-42e7-9f0e-1add393d15d0') {
                        // Build the Docker image
                        sh "docker compose up amani818/Ebankapp:latest -f docker/Dockerfile ."
                        // Push the Docker image
                        sh "docker push amani818/Ebankapp:latest"
                    }
                }
            }
        }
        stage('Trigger-cd-pipeline') {
            steps {
                build job: "CD_Pipeline1"
            }
        }
    }
}

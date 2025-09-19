pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/lakshig/8.2CDevSecOps.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building application using Maven/npm...'
            }
        }
        stage('Unit Tests') {
            steps {
                echo 'Running unit tests...'
            }
        }
        stage('SonarCloud Analysis') {
            steps {
                withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
                    sh '''
                        # Download SonarScanner if not installed
                        curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006-linux.zip
                        unzip -o sonar-scanner.zip
                        export PATH=$PATH:$(pwd)/sonar-scanner-5.0.1.3006-linux/bin

                        # Run analysis
                        sonar-scanner \
                          -Dsonar.projectKey=lakshig_8.2CDevSecOps \
                          -Dsonar.organization=lakshig \
                          -Dsonar.host.url=https://sonarcloud.io \
                          -Dsonar.login=$SONAR_TOKEN
                    '''
                }
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Running SonarQube analysis...'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running Snyk/npm audit...'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging server...'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
            }
        }
    }
}

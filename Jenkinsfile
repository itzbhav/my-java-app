pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Maven Build & Sonar') {
            steps {
                sh '''
                    # Install Maven in Docker container
                    apt-get update
                    apt-get install -y maven openjdk-17-jdk wget unzip
                    
                    # Verify Maven
                    mvn --version
                    
                    # Build
                    mvn clean compile
                    
                    # SonarQube analysis
                    withSonarQubeEnv('My Sonar Server') {
                        mvn sonar:sonar
                    }
                '''
            }
        }
    }
}

pipeline {
    agent any
    stages {
        stage('Maven Build & Sonar') {
            steps {
                sh '''
                    # Download Maven directly (no sudo needed)
                    wget -q https://archive.apache.org/dist/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz
                    tar xzf apache-maven-3.9.6-bin.tar.gz
                    export PATH=$PWD/apache-maven-3.9.6/bin:$PATH
                    
                    # Verify
                    mvn --version
                    
                    # Build
                    mvn clean compile
                    
                    # SonarQube
                    withSonarQubeEnv('My Sonar Server') {
                        mvn sonar:sonar
                    }
                '''
            }
        }
    }
}

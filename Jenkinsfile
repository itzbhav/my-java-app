pipeline {
    agent any
    stages {
        stage('Maven Build & Sonar') {
            steps {
                sh '''
                    # Use curl (exists in Jenkins Docker) instead of wget
                    curl -sL https://archive.apache.org/dist/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz -o maven.tar.gz
                    tar xzf maven.tar.gz
                    export PATH=$PWD/apache-maven-3.9.6/bin:$PATH
                    
                    # Verify Maven works
                    mvn --version
                    
                    # Clean compile
                    mvn clean compile
                    
                    # SonarQube scan
                    mvn sonar:sonar -Dsonar.host.url=http://localhost:9000
                '''
            }
        }
    }
}

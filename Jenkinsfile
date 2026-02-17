pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                    # Download Maven
                    curl -sL https://archive.apache.org/dist/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz -o maven.tar.gz
                    tar xzf maven.tar.gz
                    export PATH=$PWD/apache-maven-3.9.6/bin:$PATH
                    
                    # Build
                    mvn clean compile
                '''
            }
        }
        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv('My Sonar Server') {
                        sh '''
                            # Setup Maven again in this stage
                            export PATH=$PWD/apache-maven-3.9.6/bin:$PATH
                            
                            # Run SonarQube scan with Ubuntu host IP
                            mvn sonar:sonar \
                              -Dsonar.projectKey=my-java-app \
                              -Dsonar.projectName="My Java App" \
                              -Dsonar.host.url=http://192.168.138.78:9000
                        '''
                    }
                }
            }
        }
    }
}

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                    wget https://archive.apache.org/dist/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz
                    tar xzf apache-maven-3.9.6-bin.tar.gz
                    export PATH=$PWD/apache-maven-3.9.6/bin:$PATH
                    mvn clean compile
                '''
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('My Sonar Server') {
                    sh '''
                        wget https://archive.apache.org/dist/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz
                        tar xzf apache-maven-3.9.6-bin.tar.gz
                        export PATH=$PWD/apache-maven-3.9.6/bin:$PATH
                        mvn sonar:sonar
                    '''
                }
            }
        }
    }
}

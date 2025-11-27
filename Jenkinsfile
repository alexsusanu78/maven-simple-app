pipeline {
    agent {
            docker {
                image 'maven:3.9.6-eclipse-temurin-17'
                // args '-v $HOME/.m2:/root/.m2'           // (Optional) reuse local Maven repo for caching
            }
        }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
    }
}
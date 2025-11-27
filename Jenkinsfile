pipeline {
    agent {
        docker {
            image 'maven:3.9.9-eclipse-temurin-21'
            args '-v $HOME/.m2:/root/.m2'
        }
    }

    environment {
        MAVEN_LOCAL_REPO = '/tmp/maven-repo'
    }

    stages {
        stage('Prepare') {
            steps {
                sh 'mkdir -p $MAVEN_LOCAL_REPO'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn -Dmaven.repo.local=$MAVEN_LOCAL_REPO -B -DskipTests clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn -Dmaven.repo.local=$MAVEN_LOCAL_REPO test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
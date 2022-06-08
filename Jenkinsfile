pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '/opt/apache-maven-3.8.5/bin/mvn'
                sh 'mvn -f ./pom.xml -B -DskipTests clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts....."
                    archiveArtifacts artifacts: '**/*.jar'
                }
            }
        }
        stage('Test') {
            steps {
                sh 'mvn -f ./pom.xml test'
            }
            post {
                always {
                    junit './target/surefire-reports/*.xml'
                }
            }
        }
    }
}

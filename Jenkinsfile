pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'export M2_HOME=/opt/maven'
                export PATH=${M2_HOME}/bin:${PATH}
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

pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    options {
        timeout(10)
        buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '5', numToKeepStr: '5')
    }
    stages {
        stage('Build') {
            steps {
                sh "mvn clean compile"
            }
        }
        stage('upload artifact to nexus') {
            steps {
                sh "mvn clean package"
            }
        }
    }
    post {
        always{
            deleteDir()
        }
        failure {
            echo "sendmail -s mvn build failed receipients@my.com"
        }
        success {
            echo "The job is successful"
        }
    }
}

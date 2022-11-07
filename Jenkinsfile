pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            steps {
                echo 'Start gradle Build..'
                checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                userRemoteConfigs: [[url: 'https://github.com/jirentaicho/jenkins-test']]])
                sh 'chmod +x gradlew'
                sh './gradlew build'
                echo 'Deploy..'
                deploy adapters: [tomcat9(credentialsId: 'my-auth', path: '', url: 'http://172.31.0.2:8012/')], contextPath: 'jenkinssample', war: '**/*.war'
            }
        }
    }
}
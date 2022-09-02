pipeline {
    agent any

    stages {
        stage('CLONING FROM GIT') {
            steps {
            git branch: 'main', url: 'https://github.com/sabdulramoni/Jenkins-Simple-Build.git'
            }
        }
        stage('BUILDING WITH MAVEN') {
            steps {
                 sh 'cd SampleWebApp && mvn clean install'
            }
        }
        stage('DEPLOYING TO TOMCAT') {
            steps {
             deploy adapters: [tomcat9(credentialsId: 'tomcat-id', path: '', url: 'http://3.129.208.122:8080/')], contextPath: 'myapp', war: '**/*.war'
            }
        }
    }
}

pipeline {
    agent any

    stages {
        stage('Checkout from GIT') {
            steps {
            git branch: 'main', url: 'https://github.com/sabdulramoni/Jenkins-Simple-Build.git'
            }
        }
        stage("SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('sonar') {
                sh 'mvn -f SampleWebApp/pom.xml clean package sonar:sonar'
              }
            }
          }
        stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
        stage('BUILDING WITH MAVEN') {
            steps {
                 sh 'cd SampleWebApp && mvn clean install'
            }
        }
        stage('DEPLOY TO TOMCAT') {
            steps {
             deploy adapters: [tomcat9(credentialsId: 'tomcat-id', path: '', url: 'http://3.129.208.122:8080/')], contextPath: 'myapp', war: '**/*.war'
            }
        }
    }
}

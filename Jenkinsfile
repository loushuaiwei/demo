pipeline {
    agent any

    stages {
        stage('pull code') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/${branch}']], extensions: [], userRemoteConfigs: [[credentialsId: '508a8955-db6b-43a0-b3a5-f9a2386be59f', url: 'http://github.com/loushuaiwei/demo.git']]])
            }
        }
        stage('build project') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('publish project') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'tomcat-auth', path: '', url: 'http://192.168.1.136:8080/')], contextPath: null, war: 'target/*.war'
            }
        }
    }
}

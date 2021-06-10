pipeline {
    agent any

    stages {
        stage('pull code') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'gitee_ssh_credential', url: 'git@gitee.com:DJOSIMON/my_pipleline_proj.git']]])
            }
        }
        stage('build proj') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('publish proj') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'jenkins-to-tomcat', path: '', url: 'http://192.168.8.150:8080/')], contextPath: null, war: 'target/*.war'
            }
        }
    }
}

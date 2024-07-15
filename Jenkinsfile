pipeline {
    agent any
    tools {
        maven 'maven3'
        jdk 'java17'
    }
    stages {
        stage('git-code-download') {
            steps {
                echo "download code from git"
                git branch: 'main', url: 'https://github.com/jaybhuva30/maven-devopsstar.git'
            }
        }
        stage('build') {
            steps {
                echo "doing build"
                sh 'mvn clean package'
            }
        }
        stage('archiving-artifacts') {
            steps {
                echo "archiving the artifacts"
                archiveArtifacts artifacts: '**/target/*.war', followSymlinks: false
            }
        }
        stage('build-other-project') {
            steps {
                echo "now build other project"
                build wait: false, job: 'deploy-to-dev'
            }
        }
    }
}

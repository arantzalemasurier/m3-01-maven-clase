pipeline {
    agent any
    tools {
        maven "maven3.8.1"
        jdk "jdk16"
    }
    stages {
        stage("Env Variables") {
            steps {
                sh "printenv"
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
        stage('Sonar') {
           steps {
               sh 'mvn verify sonar:sonar -Dsonar.projectKey=arantzalemasurier_m3-01-maven-clase -Dsonar.organization=arantzalemasurier -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=6f9803ce0c72d98ab5158ad604c3b44c51ae9dd5-Dsonar.branch.name=master'
           }
        }
    }
}
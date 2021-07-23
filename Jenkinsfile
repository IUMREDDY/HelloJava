pipeline {
    agent any
    stages {
        stage('SCM') {
            steps {
                git branch: 'main', credentialsId: 'fa351df9-893c-4f9d-8b8c-3d8a26a23038', url: 'https://github.com/gvreddy1265/HelloJava.git'            }
        }
        stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                        sh '${MAVEN_HOME} clean package sonar:sonar'
                        //sh 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.login=4d1f16b44320184bcb4e78fcb5364a5832931064'
                }
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
            
        }
        }
    }
}
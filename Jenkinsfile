pipeline {
    agent any

    stages {
        stage('Build Started'){
            steps{
                //add script to send email 
                emailext body: '''For Project \'HelloJava\' the build process has been initiated. Do not reply because it is Jnekins generated auto email.''', subject: 'Build Started', to: 'gvreddy1265@gmail.com'
            }
        }
        
        stage('Clone') {
            steps {
               //add script here to clone github repository
               git branch: 'main', credentialsId: 'fa351df9-893c-4f9d-8b8c-3d8a26a23038', url: 'https://github.com/gvreddy1265/HelloJava.git'
            }
        }
        
        stage('Compile'){
            steps{
                //add script here to compile the maven project
                sh '${MAVEN_HOME} clean compile'
            }
        }
        
        stage('Test'){
            steps{
                //add a step to run the maven tests
                sh '${MAVEN_HOME} clean test'
            }
        }
        
        stage('Package'){
            steps{
                //add a step to pacakge jar file
                sh '${MAVEN_HOME} clean package'
            }
        }
        
        stage('Publish to Nexus'){
            steps{
                //add a script to publish jar file into Nexus Repository
                sh '${MAVEN_HOME} -s ./setting.xml deploy'
            }
        }
    }
}

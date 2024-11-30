
pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "mvn_home"
    }

    stages {
        
         stage('Initialize spboot'){
            steps{
                echo "PATH = ${M2_HOME}/bin:${PATH}"
                echo "mvn_home = /opt/apache-maven-3.9.9"
            }
        }
        
        stage('git checkout') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/ayushpratapsingh/spbmavenexample.git'
                
            }
        }
        
        stage('compile sc') {
            steps {
               sh "mvn compile"
            }
        }  
        
        stage('test sc') {
            steps {
               sh "mvn test"
               }
        }
        
        stage('package sc') {
            steps {
               sh "mvn clean package"
            }
        }
        
        stage('Deploy war') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcatads', path: '', url: 'http://18.212.217.2:8080/')], contextPath: 'myapp', onFailure: false, war: 'target/*.war'
             }
        }  
        
    }
    post {

        success {

            archiveArtifacts artifacts: 'target/*.war'  // Example: archive all .jar files in the 'target' folder

        }

    }
            
}

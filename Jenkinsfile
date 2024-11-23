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
        
        stage('Build spboot') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/ayushpratapsingh/spbmavenexample.git'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
            
        stage("archive as war")
        {
            steps{
            archiveArtifacts artifacts: 'target/*.war', followSymlinks: false
            }
            
        }
        stage("deploy to container"){
            steps{
            
                deploy adapters: [tomcat9(credentialsId: 'tomcatads', path: '', url: 'http://18.212.202.239:8080/')], contextPath: 'hellocp', war: 'target/*.war'
            }
            }
        
            
        }
            
        }

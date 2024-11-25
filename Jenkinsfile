pipeline {
    agent any 
    tools {
         maven 'maven'
         jdk 'java'
    }
    stages {
         stage('Stage-0 : Static Code Analysis Using SonarQube') { 
           steps {
                sh 'mvn clean verify sonar:sonar -DskipTests'
            }
        }
        stage('Stage-1 : Clean') { 
            steps {
                sh 'mvn clean'
            }
        }
         stage('Stage-2 : Validate') { 
            steps {
                sh 'mvn validate'
            }
        }
         stage('Stage-3 : Compile') { 
            steps {
                sh 'mvn compile'
            }
        }
         stage('Stage-4 : Test') { 
            steps {
                sh 'mvn test '
            }
        }
          stage('Stage-5 : package') { 
            steps {
                sh 'mvn package '
            }
        }
          stage('Stage-6 : Verify') { 
            steps {
                sh 'mvn verify '
            }
        }
          stage('Stage-7 : install') { 
            steps {
                sh 'mvn install '
            }
        }
          stage('Stage-8 : Deploy an Artifact to Artifactory Manager i.e. Nexus/Jfrog') { 
            steps {
                sh 'mvn deploy'
            }
        }

          stage('Stage-9 : Deployment - Deploy a Artifact Calculator-1.0.0-SNAPSHOT.war file to Tomcat Server') { 
            steps {
                sh 'curl -u admin:redhat@123 -T target/**.war "http://52.91.175.212:8080/manager/text/deploy?path=/Calculator&update=true"'
            }
        } 
  
          stage('Stage-10 : SmokeTest') { 
            steps {
                sh 'curl --retry-delay 10 --retry 5 "http://52.91.175.212:8080/Calculator"'
            }
        }
    }
}

pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                sh '/scratch/wcpbt/software/maven/apache-maven-3.9.4/bin/mvn -f java-tomcat-sample-docker/pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
 
        stage('Create Tomcat Docker Image'){
            steps {
                sh "docker build . -t tomcatsamplewebapp:${env.BUILD_ID}"
            }
        }
 
    }
}

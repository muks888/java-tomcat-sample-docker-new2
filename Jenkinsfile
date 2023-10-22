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
                sh 'export HTTPS_PROXY=http://www-proxy.us.oracle.com:80;export https_proxy=http://www-proxy.us.oracle.com:80;export NO_PROXY=localhost,127.0.0.1,.us.oracle.com,.oraclecorp.com,/var/run/docker.sock;export no_proxy=localhost,127.0.0.1,.us.oracle.com,.oraclecorp.com,/var/run/docker.sock;export HTTP_PROXY=http://www-proxy.us.oracle.com:80;export http_proxy=http://www-proxy.us.oracle.com:80'
                sh "/usr/local/packages/aime/install/run_as_root 'docker build . -t tomcatsamplewebapp:${env.BUILD_ID}'"
            }
        }
 
    }
}

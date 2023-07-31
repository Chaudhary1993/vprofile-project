pipeline {
    
	agent any
	
	tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }

    environment {
        SNAP_REPO = "vprofile-snapshot"
        NEXUS_USER = "admin"
        NEXUS_PASS = "admin"
        RELEASE_REPO = "vprofile-release"
        CENTRAL_REPO = "vpro-maven-central"
        NEXUSIP = "172.31.40.24"
        NEXUSPORT = "8081"
        NEXUS_GRP_REPO = "vpro-maven-group"
        NEXUS_LOGIN= 'nexuslogin'
        SONARSERVER= 'sonarserver'
        SONARSCANNER='sonarscanner'
    }
	
    stages { 
        
        stage('Build') {
            steps {
                sh 'mvn clean install -DskipTests -s settings.xml'
            }
            post {
                success {
                  echo "Now Archiving"
                  archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Test'){
            steps{
                sh 'mvn test -s settings.xml'
            }
        }
        stage('Checkstyle Analysis'){
            steps{
               sh 'mvn checkstyle:checkstyle -s settings.xml'
            }
        }
        stage('Sonar Analysis'){
          environment{
            scannerHome = tool "${SONARSCANNER}"
          }
          steps{
            withSonarQubeEnv("${SONARSERVER}") {
               sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                   -Dsonar.projectName=vprofile-project \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
            }
          }
        }
    }

}

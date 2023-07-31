pipeline {
    
	agent any
	
	tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }

    environment {
        SNAP-REPO = "vprofile-snapshot"
        NEXUS-USER = "admin"
        NEXUS-PASS = "admin"
        RELEASE-REPO = "vprofile-release"
        CENTRAL-REPO = "vpro-maven-central"
        NEXUSIP = "172.31.40.24"
        NEXUSPORT = "8081"
        NEXUS-GRP-REPO = "vprofile-grp-repo"
        NEXUS-LOGIN= 'nexuslogin'
    }
	
    stages{
        
        stage('BUILD'){
            steps {
                sh 'mvn clean install -DskipTests'
            }     
        }

    }


}

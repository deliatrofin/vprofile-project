pipeline {
    agent any
    tools {
        maven "MAVEN3.9.14"
        jdk "JDK21"
    }
    
    environment {
        SNAP_REPO = 'vprofile-snapshot'
		NEXUS_USER = 'admin'
		NEXUS_PASS = 'Alint@roma1!'
		RELEASE_REPO = 'vprofile-release'
		CENTRAL_REPO = 'vpro-maven-central'
		NEXUSIP = '172.31.19.22'
		NEXUSPORT = '8081'
		NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
    }

    stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post{
                success{
                    echo "Now archiving the artifacts"
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
         stage('Checkstyle Analysis') {
            steps {
                
                    sh 'mvn checkstyle:checkstyle'
            }
        }
       
    }
}
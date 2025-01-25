pipeline{
    agent any
    tools{
        maven 'MAVEN3'
        jdk 'OracleJDK21'
    }
    environment {
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'Versman1@gloria'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vprofile-maven-central'
        NEXUSIP = '172.31.2.75'
        NEXUSPORT = '8081'
        NEXUS_GRP_REPO = 'vprofile-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -U clean install'
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post {
                success {
                    echo('now archiving')
                    archiveArtifacts(artifacts: '**/*.war')
                }
            }
        }
        stage('Test') {
            steps {
                sh 'mvn -s mvn test'
            }
        }
        stage('Checkstyle Analysis') {
            steps {
                sh 'mvn -s mvn checkstyle:checkstyle'
            }
        }
    }
}

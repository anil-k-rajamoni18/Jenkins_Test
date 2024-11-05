pipeline {
    agent {
        label 'linuxSlave'
    }

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "MVN3"
    }

    stages {
        stage('pull SCM') {
            steps {
                // Get some code from a GitHub repository
                git credentialsId: 'git', url: 'git@github.com:anil-k-rajamoni18/Jenkins_Test.git'
            }
        }
        
        stage('Build') {
            steps {
                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true -f api-gateway/ clean install"
            }
        }
        
        stage('publish artifact') {
            steps {
                archiveArtifacts 'api-gateway/target/*.jar'
            }
        }
        
        stage('Publish junit result') {
            steps {
                junit 'api-gateway/target/surefire-reports/*.xml'
            }
        }

    }
}

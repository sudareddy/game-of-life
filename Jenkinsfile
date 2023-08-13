pipeline {
    agent { label 'JDK_17' }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/sudareddy/game-of-life.git',
                    branch: 'declarative'
            }
        }
        stage('package') {
            steps {
                        sh 'export PATH="/usr/lib/jvm/java-1.8.0-openjdk-amd64/bin:$PATH" && mvn package'
            }
        }
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/target/gameoflife.war',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}
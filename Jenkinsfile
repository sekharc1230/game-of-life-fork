pipeline {
    agent { label 'java-app' }
    triggers { pollSCM ('H/30 * * * *') }
    parameters {
        choice(name: 'MAVEN_GOAL', choices: ['package', 'install', 'clean'], description: 'Maven Goal')
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/sekharc1230/game-of-life-fork.git',
                branch: 'master'
            }
        }
        stage('package') {
            tools {
                jdk 'JDK_8'
            }
            steps {
                sh "mvn ${params.MAVEN_GOAL}"
            }
        }
        stage('postbuild') {
            steps {
                archiveArtifacts artifacts: '**/target/gameoflife.war',
                               onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'               
            }
        }
    }
}
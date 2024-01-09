node('java-applications') {
    stage('vcs') {
        git url: 'https://github.com/sekharc1230/game-of-life-fork.git',
           branch: 'scripted'
    }
    stage('archive the artifacts') {
        archiveArtifacts onlyIfSuccessful: true,
        artifacts : '**/target/gameoflife.war',
        allowEmptyArchive: false
    }
    stage('show the test results') {
        junit testResults: '**/surefire-reports/TEST-*.xml',
        allowEmptyResults: 'true'
    }
}
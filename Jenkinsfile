pipeline {
    agent any
    environment {
        KATALON_API_KEY = credentials('katalon-api-key')
    }
    stages {
        stage('Test') {
            steps {
                sh '''
                    katalonc -noSplash -runMode=console \
                    -projectPath="$(pwd)" \
                    -retry=0 -testSuitePath="Test Suites/TS_RegressionTest" \
                    -executionProfile="default" \
                    -browserType="Chrome (headless)" \
                    -apiKey=${KATALON_API_KEY}
                '''
            }
        }
    }
    post {
        always {
            script {
                if (fileExists('Reports')) {
                    archiveArtifacts artifacts: 'Reports/**/*.*', fingerprint: true, allowEmptyArchive: true
                }
                if (fileExists('Reports/**/JUnit_Report.xml')) {
                    junit 'Reports/**/JUnit_Report.xml'
                }
            }
        }
    }
}

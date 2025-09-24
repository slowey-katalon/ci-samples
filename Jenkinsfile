pipeline {
    agent any
    environment {
        KATALON_API_KEY = credentials('katalon-api-key')
        KATALON_APP_PATH = '/Applications/Katalon Studio Engine v10.3.1.app/Contents'
    }
    stages {
        stage('Test') {
            steps {
                dir('.') {  
                    sh '''
                        "${KATALON_APP_PATH}/MacOS/katalonc" \
                        -noSplash \
                        -runMode=console \
                        -projectPath="$(pwd)" \
                        -retry=0 \
                        -statusDelay=15 \
                        -testSuitePath="Test Suites/TS_RegressionTest" \
                        -browserType="Chrome" \
                        -apiKey="${KATALON_API_KEY}"
                    '''
                }
            }
        }
    }
    post {
        always {
            script {
                // Archive reports from root directory
                if (fileExists('Reports')) {
                    archiveArtifacts artifacts: 'Reports/**/*.*', fingerprint: true, allowEmptyArchive: true
                } else {
                    echo 'No Reports directory found'
                }
                
                if (fileExists('Reports/**/JUnit_Report.xml')) {
                    junit 'Reports/**/JUnit_Report.xml'
                } else {
                    echo 'No JUnit report files found'
                }
            }
        }
    }
}

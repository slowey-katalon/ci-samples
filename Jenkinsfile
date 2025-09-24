pipeline {
    agent any
    environment {
        KATALON_API_KEY = credentials('katalon-api-key') // Set this credential in Jenkins
        KATALON_APP_PATH = '/Applications/Katalon Studio Engine v10.3.1.app/Contents'
    }
    stages {
        stage('Test') {
            steps {
                dir('<your-project-folder>') {  // Replace with your actual project folder name
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
}

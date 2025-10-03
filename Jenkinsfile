pipeline {
    agent any

    stages {
        stage('Run JMeter Test') {
            steps {
                echo 'Running JMeter test...'

                // Run the test
                sh '''
                    mkdir -p reports
                    jmeter -n -t tests/performance/FullFlow.jmx -l reports/result.jtl -e -o reports/html
                '''
            }
        }

        stage('Publish Report') {
            steps {
                publishHTML([
                    allowMissing: false,
                    alwaysLinkToLastBuild: true,
                    keepAll: true,
                    reportDir: 'reports/html',
                    reportFiles: 'index.html',
                    reportName: 'JMeter Performance Report'
                ])
            }
        }
    }
}

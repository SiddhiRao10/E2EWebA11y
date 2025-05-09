pipeline {
    agent any

    environment {
        BROWSERSTACK_USERNAME = credentials('browserstack-username')
        BROWSERSTACK_ACCESS_KEY = credentials('browserstack-access-key')
        BROWSERSTACK_CONFIG_FILE = 'src/test/resources/conf/capabilities/browserstack.yml'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/SiddhiRao10/E2EWebA11y.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('Run Tests on BrowserStack') {
            steps {
                sh 'mvn clean test -P bstack-parallel-browsers'
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
        }
        success {
            echo '✅ Tests passed!'
        }
        failure {
            echo '❌ Tests failed!'
            currentBuild.result = 'FAILURE'
        }
    }
}

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
                script {
                    // Manually checkout the correct branch
                    sh 'git checkout e2e-web-demo'
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '/Users/siddhirao/Downloads/apache-maven-3.9.9/bin/mvn clean install -DskipTests'

            }
        }

        stage('Run Tests on BrowserStack') {
            steps {
                    sh '/Users/siddhirao/Downloads/apache-maven-3.9.9/bin/mvn clean test -P bstack-parallel-browsers'
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
        }
    }
}

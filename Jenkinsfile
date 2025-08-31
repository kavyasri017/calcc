pipeline {
    agent any

    triggers {
        githubPush()
    }

    tools {
        // Install the Maven version configured as "M3" in Jenkins Global Tool Configuration
        maven "M3"
    }

    stages {
        stage('Build') {
            steps {
                // Checkout source code
                git branch: 'main', url: 'https://github.com/kavyasri017/calcc.git'

                // Run Maven build
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
    }

    post {
        success {
            // Publish test results and artifacts
            junit '**/target/surefire-reports/TEST-*.xml'
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
    }
}

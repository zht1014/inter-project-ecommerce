/* pipeline {
    agent any
    tools { 
        nodejs 'node18' // 使用 Jenkins 配置的 Node.js 版本
    }
    stages {
        stage('Build') {
            steps {
                sh 'node -v'    // 确保 Node.js 版本正确
                sh 'npm install'
            }
        }
    }
} */

pipeline {
    agent any
    tools { 
        nodejs 'node18' // 使用 Jenkins 配置的 Node.js 版本
    }
    environment { 
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'chmod +x jenkins/scripts/test.sh'
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') { 
            steps {
                sh 'chmod +x jenkins/scripts/deliver.sh'
                sh './jenkins/scripts/deliver.sh' 
                input message: 'Finished using the web site? (Click "Proceed" to continue)' 
                sh 'chmod +x jenkins/scripts/kill.sh'
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}
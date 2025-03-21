pipeline {
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
}
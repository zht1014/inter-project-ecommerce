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

/* pipeline {
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

                // 启动临时 Node.js 服务器
                sh 'nohup npm start -- --host 0.0.0.0 --port 3000 > node_app.log 2>&1 &'
                
                // 等待服务器启动
                sleep 5

                // Jenkins 交互等待，允许用户手动测试
                input message: 'Finished using the web site? (Click "Proceed" to continue)' 

                // 结束 Node.js 进程
                sh 'chmod +x jenkins/scripts/kill.sh'
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}

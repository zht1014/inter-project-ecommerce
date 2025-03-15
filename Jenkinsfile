pipeline {
    agent any

    environment {
        // 设置 Node.js 环境
        NODEJS_HOME = tool name: 'NodeJS 20', type: 'nodejs'
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                // 使用 SSH URL 拉取代码
                git branch: 'master', url: 'git@github.com:zht1014/inter-project-ecommerce.git', credentialsId: 'github-jenkinstest-ssh-key'
            }
        }

        stage('Install Dependencies') {
            steps {
                // 安装项目依赖
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                // 构建项目
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                // 部署到服务器（示例：将构建结果复制到指定目录）
                sh 'cp -r build/* /var/www/html'
            }
        }
    }
}
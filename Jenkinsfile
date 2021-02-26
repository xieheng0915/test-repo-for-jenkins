pipeline {
    agent any
    triggers {
        // 毎日22時に実行（変更箇所）
        pollSCM('H/15 * * * *')
    }
    // 環境変数を設定します
    environment {
        //Gitlabのプロジェクトのgit URL　（変更箇所）
        SCMURL = 'https://github.com/xieheng0915/test-repo-for-jenkins.git'
    }
    // 処理
    stages {
        // ビルド
        stage('checkout') {
            steps {
                // ソースのチェックアウト
                git url: SCMURL
            }
        }
        // ユニットテスト実行
        /*
        stage('test-phing') {
            steps {
                // composerのユニットテストイベントを呼び出す
                sh 'phing'
            }
        }
        */
        // 静的な解析
        stage('sonar scanner') {
            steps {
                // composerの静的解析イベントを呼び出す
                sh '/opt/sonar-scanner/bin/sonar-scanner \
                    -Dsonar.login=088db75e7448875d6072564eb8839933b071caf3'
            }
        }
        
    }
    post {
        // stagesの処理が成功した場合に実行する処理
        success {
            // ワークスペースをクリーン
            cleanWs()
        }
    }
}
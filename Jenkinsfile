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
        // 静的解析の実行 by sonar-scanner
        /*
        stage('check') {
            steps {
                // composerの静的解析イベントを呼び出す
                sh 'sonar-scanner -Dsonar.login=ee858ccab609a4dac97697e0636fe344d86d356d'
            }
        }*/

        // ユニットテスト実行
        stage('test-phing') {
            steps {
                // composerのユニットテストイベントを呼び出す
                sh 'phing'
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
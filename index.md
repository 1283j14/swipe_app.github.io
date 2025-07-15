<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Spotify認証完了</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 600px;
            margin: 50px auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        .container {
            background-color: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            text-align: center;
        }
        .success {
            color: #1DB954;
            font-size: 24px;
            margin-bottom: 20px;
        }
        .url-display {
            background-color: #f0f0f0;
            padding: 15px;
            border-radius: 5px;
            word-break: break-all;
            font-family: monospace;
            font-size: 14px;
            margin: 20px 0;
        }
        .copy-button {
            background-color: #1DB954;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }
        .copy-button:hover {
            background-color: #1ed760;
        }
        .instructions {
            margin-top: 20px;
            text-align: left;
            line-height: 1.6;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="success">✅ Spotify認証が完了しました！</div>
        
        <p>以下のURLをコピーして、アプリケーションのダイアログに貼り付けてください：</p>
        
        <div class="url-display" id="currentUrl">
            読み込み中...
        </div>
        
        <button class="copy-button" onclick="copyUrl()">URLをコピー</button>
        
        <div class="instructions">
            <h3>手順：</h3>
            <ol>
                <li>上記の「URLをコピー」ボタンをクリック</li>
                <li>アプリケーションのダイアログに戻る</li>
                <li>コピーしたURLを貼り付けて「認証コードを送信」をクリック</li>
            </ol>
        </div>
    </div>

    <script>
        // ページが読み込まれた時に現在のURLを表示
        window.onload = function() {
            const currentUrl = window.location.href;
            document.getElementById('currentUrl').textContent = currentUrl;
        };

        // URLをクリップボードにコピーする関数
        function copyUrl() {
            const url = window.location.href;
            navigator.clipboard.writeText(url).then(function() {
                alert('URLがクリップボードにコピーされました！');
            }).catch(function(err) {
                // フォールバック: テキストを選択状態にする
                const urlDisplay = document.getElementById('currentUrl');
                const range = document.createRange();
                range.selectNode(urlDisplay);
                window.getSelection().removeAllRanges();
                window.getSelection().addRange(range);
                alert('URLを選択しました。Ctrl+Cでコピーしてください。');
            });
        }
    </script>
</body>
</html>

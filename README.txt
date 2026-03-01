# 底値メモ - セットアップ方法

## ファイル構成
```
底値メモ/
├── index.html          # メインアプリ
├── manifest.json       # PWA設定
├── service-worker.js   # オフライン対応
└── icons/
    ├── icon-192.png
    └── icon-512.png
```

## iPhoneでPWAとして使う方法

### まず結論（よくある質問）
- `https://github.com/kusamoti1/Public`（リポジトリ画面）を開くだけでは、PWAとしては動きません。
- **GitHub Pages の公開URL** を開いてください。
  - このリポジトリなら通常は **`https://kusamoti1.github.io/Public/`** です。

### ステップ1: GitHub Pages を有効化する
1. リポジトリ `Public` を開く
2. **Settings > Pages** を開く
3. **Build and deployment** の Source を **Deploy from a branch** にする
4. Branch を **main / (root)** にして Save
5. 数十秒〜数分待って、表示された公開URL（例: `https://kusamoti1.github.io/Public/`）にアクセス

> 補足: 404になる場合は、反映待ちのことが多いので少し待って再読み込みしてください。

### ステップ2: ホーム画面に追加
1. iPhone の **Safari** で公開URLを開く
2. 下の共有ボタン（□↑）をタップ
3. **「ホーム画面に追加」** をタップ
4. 名前を確認して「追加」

これでアプリとして使えます。オフラインでも動作します。

## 代替: ローカルサーバで試す（PCとiPhoneが同じWi-Fi）
```bash
cd 底値メモ
python -m http.server 8080
```
iPhoneのSafariで `http://PCのIPアドレス:8080` にアクセス

## データについて
- データはiPhone/ブラウザのlocalStorageに保存
- ブラウザのデータを削除するとデータも消えます
- 定期的に「データ管理」タブからJSONエクスポートをおすすめします


## PRで「conflicts」が出るとき
- はい、ほとんどの場合は **PRブランチが古い（base/mainの更新を取り込めていない）** ことが原因です。
- これはアプリ不具合ではなく、**同じファイルの同じ行付近を別ブランチで編集した差分競合**です。

### スマホでの確認ポイント
1. PR画面を再読み込みする（Safariを引っ張って更新）
2. PRの最新コミット時刻が「今」の更新になっているか確認
3. まだ競合が出る場合は、`README.md` / `APP_IMPROVEMENT_PROPOSAL.md` など同じファイルを両方で触っている可能性が高い

### 解消方法（どちらか）
- GitHubの「対立を解決する」ボタンから解決してコミット
- もしくは、PRブランチに main の最新を取り込んでから再push

> 補足: 競合表示はキャッシュで古く見えることがあるため、再読み込み後に再確認してください。


## 「ブランチを更新する」で500エラーが出るとき
- これはGitHub側の一時エラー（サーバー混雑やモバイルWebの不安定動作）で起きることがあります。
- **あなたの操作ミスとは限りません**。同じ操作でも時間をおくと通ることがあります。

### まず試す順番（iPhone）
1. PR画面を完全再読み込み（Safari更新）
2. いったんPR画面を閉じて開き直す
3. 数分あけて再実行（特に 500 は再試行で直ることが多い）
4. 可能ならPCブラウザから「Update branch」を実行

### 毎回起こる場合の予防策
- PRは**1本ずつ**マージして、次の作業ブランチは最新mainから作る
- 何度も変わるファイル（`README.md` など）は、別PRと同時に触らない
- 大きな変更を分割してPRを小さくする（競合と更新失敗を減らせます）

### それでもダメなとき
- 「Update branch」を使わず、ローカルで main を取り込んでpushするのが確実です。
  - 例: `git fetch` → `git rebase origin/main`（または `git merge origin/main`）→ `git push`

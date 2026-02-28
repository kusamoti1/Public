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

### ステップ1: ファイルをサーバに置く
PWAはhttpsまたはlocalhostで動作します。以下のいずれかの方法を使ってください。

**方法A: GitHub Pages（無料）**
1. GitHubアカウントを作成
2. 新しいリポジトリを作成（publicにする）
3. 全ファイルをアップロード
4. Settings > Pages > Source: main branch
5. https://ユーザー名.github.io/リポジトリ名/ にアクセス

**方法B: ローカルサーバ（PCとiPhoneが同じWi-Fi）**
```bash
cd 底値メモ
python -m http.server 8080
```
iPhoneのSafariで `http://PCのIPアドレス:8080` にアクセス

### ステップ2: ホーム画面に追加
1. SafariでURLを開く
2. 下の共有ボタン（□↑）をタップ
3.「ホーム画面に追加」をタップ
4. 名前を確認して「追加」

これでアプリとして使えます。オフラインでも動作します。

## データについて
- データはiPhone/ブラウザのlocalStorageに保存
- ブラウザのデータを削除するとデータも消えます
- 定期的に「データ管理」タブからJSONエクスポートをおすすめします

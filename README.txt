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

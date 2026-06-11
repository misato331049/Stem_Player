# 🎛 Stem Player

ステム対応の音楽プレイヤーサイトです。  
ユーザーは楽曲をステム単位でソロ・ミュートして聴けます。

---

## ファイル構成

```
/
├── index.html      ← ユーザー向け（楽曲一覧 + ステムプレイヤー）
├── admin.html      ← 管理者向け（楽曲追加・編集・削除）
├── songs.json      ← 楽曲データ（自動更新）
└── stems/          ← ステムファイル（自動アップロード）
    └── song-title/
        ├── drums.mp3
        └── bass.mp3
```

---

## セットアップ

### 1. GitHub リポジトリを作る

1. GitHub で **Public** または **Private** リポジトリを新規作成
2. このフォルダの内容をそのままプッシュ

```bash
git init
git add .
git commit -m "init"
git remote add origin https://github.com/yourname/your-repo.git
git push -u origin main
```

### 2. Netlify / Vercel にデプロイ

- **Netlify**: [netlify.com](https://netlify.com) → "Add new site" → GitHub リポジトリを選択 → Deploy
- **Vercel**: [vercel.com](https://vercel.com) → "New Project" → GitHub リポジトリを選択 → Deploy

GitHub と連携しておくと、`songs.json` が更新されるたびに**自動で再デプロイ**されます。

### 3. GitHub Personal Access Token を発行

1. https://github.com/settings/tokens/new を開く
2. スコープ: **`repo`** にチェック
3. トークンをコピー（`ghp_xxxx...`）

### 4. admin.html を開いて設定

1. デプロイ済みの `https://your-site.com/admin.html` にアクセス
2. 左下の「設定を変更」をクリック
3. Token・リポジトリ名（`yourname/your-repo`）・ブランチを入力して保存

---

## 使い方（管理者）

1. `admin.html` を開く
2. 「楽曲を追加」→ タイトル・アーティスト名を入力
3. ステムファイル（MP3/WAV/OGG）をアップロード
4. ステム名を確認して「保存して公開」

保存すると自動で：
- ステムファイルが GitHub の `stems/` に保存される
- `songs.json` が更新される
- Netlify/Vercel が自動再デプロイ → ユーザーページに反映

---

## songs.json の形式

```json
[
  {
    "id": "abc123",
    "title": "曲名",
    "artist": "アーティスト名",
    "artwork": "https://example.com/art.jpg",
    "stems": [
      { "name": "Drums",  "file": "stems/song-title/drums.mp3" },
      { "name": "Bass",   "file": "stems/song-title/bass.mp3" },
      { "name": "Vocals", "file": "stems/song-title/vocals.mp3" }
    ]
  }
]
```

---

## 注意事項

- ステムファイルは**同じ長さ・同じテンポ**で揃えてください
- GitHub の無料プランでは1ファイル最大 **100MB** まで
- 大容量ファイルは [Git LFS](https://git-lfs.github.com/) の使用を推奨
- `admin.html` のアクセス制限は URL を知っている人のみです（認証なし）。必要に応じて Netlify の Password Protection を使ってください

# ゆきがっせん.io ❄

ブラウザで遊べるオンライン雪合戦(リアルタイムアクション)。
**完全無料**で動きます — サーバー不要、WebRTC(P2P)で直接通信します。

## 遊び方

1. 誰かが「部屋を作る」→ 4文字の部屋コードが表示される
2. 友達が同じURLを開いてコードを入力(または招待リンクから参加)
3. PC: WASD移動+クリックで雪玉 / スマホ: 左ドラッグ移動+右タップで雪玉
4. 動くとおおきくなり(弾も強くなる)、当たるか投げるとちいさくなる。ちいさくなりすぎたらやられ
5. とてもおおきくなると一撃必殺・貫通の「最強雪玉」が撃てる(撃つと初期サイズに戻る)
6. でかい雪玉は着弾で3つに分裂。マップにはときどき大雪玉(即+10サイズ)が出現
7. 3ポイント先取でラウンド勝利 → 自動で次ラウンド
8. 1人のときは強いCPUが相手をしてくれる。ホストが退出しても自動で引き継ぎ

## 無料デプロイ手順(GitHub + Vercel)

### 1. GitHubにpush

```bash
git init
git add .
git commit -m "snowfight game"
# GitHubで空リポジトリを作成してから:
git remote add origin https://github.com/<あなたのユーザー名>/snowfight.git
git push -u origin main
```

### 2. Vercelにデプロイ

1. [vercel.com](https://vercel.com) にGitHubアカウントでログイン(無料のHobbyプラン)
2. **Add New → Project** → 作ったリポジトリを **Import**
3. Framework Preset は **Other** のまま、設定変更なしで **Deploy**
4. 発行されたURL(`https://xxx.vercel.app`)を友達に共有すれば完成

以降は `git push` するだけで自動で再デプロイされます。

> 静的ファイル1枚なので、GitHub Pages(Settings → Pages)でも同様に無料公開できます。

## 仕組み

- ホスティング: Vercel(静的HTML、無料枠)
- 通信: [PeerJS](https://peerjs.com)(WebRTC P2P)。シグナリングはPeerJSの無料公開サーバーを利用
- 構成: ホストのブラウザが中継役(スター型)。ホストが退出すると部屋は解散
- Vercelの無料枠では常時起動のWebSocketサーバーを持てないため、P2P構成にしています

## 制限・注意

- 一部の厳しいNAT/社内ネットワークではP2P接続に失敗することがあります(TURNサーバーなしのため)
- 推奨人数は2〜6人。PCのキーボード+マウス操作前提です

## 発展アイデア

- Supabase Realtime(無料枠)に置き換えてホスト不在でも部屋を維持
- モバイル用バーチャルパッド対応
- アイテム(スピードアップ、大玉)の追加

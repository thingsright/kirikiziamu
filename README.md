# きりきざむ — strip glitch editor

画像を短冊状に切り刻み、ずらし・回し・ゆがめて再構成するグリッチアートツール。
ブラウザだけで動作する単一HTMLファイル。インストール不要。

**[→ Live Demo](https://your-username.github.io/kirikiziamu/)**

---

## 特徴

**8つの動かしかた** — 交互・なみうつ・のこぎり・きざむ・ジグザグ・グルグル・跳ね飛ばす・でたらめ

**20以上のパラメータ** — ストリップ幅、ズレ、回転、ねじれ、遠近感、横つぶし、かしげ、楕円軌道 etc.

**RGBチャンネル分離** — R/G/Bを独立にずらすグリッチ表現の核

**色相回転** — ストリップごとに累積するhue-rotateで虹のグラデーション

**リアルタイムアニメーション** — Space キーで再生/停止、速度調整可能

**8つの型（プリセット）** — 静寂の裂け目、水面の記憶、都市の断層、夢のほつれ、風に溶ける、万華鏡、時の歪み、ノイズの海

**透明背景書き出し** — PNG alpha対応

## キーボード

| キー | 操作 |
|------|------|
| `Space` | アニメーション再生/停止 |
| `R` | 乱数をふりなおす |
| `S` | PNG保存 |

## 使い方

1. `index.html` をブラウザで開く
2. 画像をドロップまたはクリックして選択
3. パラメータを調整
4. `↓ 保存` で原寸PNGをダウンロード

## パフォーマンス設計

プレビューは最長辺640pxにスケーリングし、保存時のみ原寸で描画します。アニメーション中は重い `ctx.filter`（hue-rotate）をCSS近似に切り替え、30fps制限で安定した操作感を保ちます。RGBチャンネル分離はポストプロセス方式（N回描画 → チャンネル分解 → lighter合成）で、旧方式の3N回描画から大幅に軽量化しています。

## セットアップ（GitHub Pages）

```bash
git init kirikiziamu && cd kirikiziamu
cp /path/to/index.html .
cp /path/to/README.md .
git add -A && git commit -m "initial release"
gh repo create kirikiziamu --public --source=. --push
gh api repos/{owner}/{repo}/pages -X POST -f source.branch=main -f source.path=/
```

数分後に `https://your-username.github.io/kirikiziamu/` で公開されます。

## ライセンス

MIT

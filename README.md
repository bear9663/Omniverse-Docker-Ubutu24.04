#  Omniverse Docker Environment（Isaac Sim + USD Composer）

このリポジトリは、**NVIDIA Omniverse Isaac Sim 4.5.0** および  
**USD Composer 2024.1** を、GUI 対応の Docker 環境上で簡単に起動できるテンプレートです。

Docker が使える Ubuntu 環境であれば、**ワンコマンドで起動**できます。

---

##  同梱イメージ（GHCR）

| コンテナ名     | バージョン  | GHCR パス |
|---------------|-------------|------------|
| Isaac Sim     | `4.5.0`     | [`ghcr.io/bear9663/isaac-sim:4.5.0`](https://github.com/users/bear9663/packages/container/isaac-sim) |
| USD Composer  | `2024.1`    | [`ghcr.io/bear9663/usd-composer:latest`](https://github.com/users/bear9663/packages/container/usd-composer) |

---

## 対応環境

| 項目       | 内容                      |
|------------|---------------------------|
| OS         | Ubuntu 22.04 / 24.04     |
| GPU        | NVIDIA GPU（RTX / A6000 など） |
| Docker     | 24.x 推奨（compose v2 対応） |
| X11        | GUI をホスト側で使えること |
| CUDA       | 11.8 以上（Host にインストール済み） |

---

##  セットアップ手順

###  1. リポジトリを clone

```bash
git clone https://github.com/bear9663/omniverse-docker.git
cd omniverse-docker
cp .env.example .env        # 初期設定（DISPLAY など）をコピー
```

###  2. GUI 用環境変数のセット（毎回）

```bash
export DISPLAY=:1           # 必要に応じて :0 や :0.0
xhost +local:root           # root アクセス許可
```

###  3. 起動

```bash
docker compose up -d isaac-sim usd-composer
```

GUI ウィンドウ（Isaac Sim / USD Composer）が表示されれば成功です。

---

##  停止・削除

```bash
docker compose down         # 停止
docker compose down -v      # 停止＋ボリューム削除
```

---

##  フォルダ構成（参考）

```
omniverse-docker/
├── docker-compose.yml
├── .env.example
├── README.md
├── usd-composer/
│   └── Dockerfile          # Composer の build 用
```

---

##  よくある質問

### Q. GUI が表示されない／真っ暗です  
→ `DISPLAY` の設定や `xhost` が漏れていないか確認してください。

```bash
echo $DISPLAY
xhost +local:root
```

### Q. GPU を使っているか確認したい  
→ `nvidia-smi` や `docker stats` で確認可能です。

---

##  関連リンク

- [Isaac Sim 公式ドキュメント](https://docs.omniverse.nvidia.com/isaacsim/latest/index.html)
- [USD Composer 公式ページ](https://developer.nvidia.com/usd-composer)
- [GitHub Packages (GHCR)](https://github.com/bear9663?tab=packages)

---

##  制作・公開

**Author**: [bear9663](https://github.com/bear9663)  

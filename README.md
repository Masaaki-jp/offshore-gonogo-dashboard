# Offshore Go/No-Go Dashboard (GAS)
**洋上風力・実務向けマイクロ気象ダッシュボード**

[English](#english) | [日本語](#japanese)

---

<a id="english"></a>
## 🌐 English

### 🌊 About The Project
This project is a lightweight, automated weather monitoring dashboard built with Google Apps Script (GAS) and Google Sheets. It is designed to support Go/No-Go decision-making for offshore wind farm operations (e.g., vessel transfers, crane operations, drone inspections) by monitoring micro-weather and wave conditions.

### 📊 Live Demo
You can check the actual working dashboard or copy it to your Google Drive to see the GAS code in action.
* 👁️ [**View Live Dashboard (Read-only)**](https://docs.google.com/spreadsheets/d/1BEvN0FNI-cV6G_C72O_4tgWIL5GeA0p6Ml2j-muf5EY/edit?usp=sharing)
* 📋 [**Make a Copy to test GAS (Requires Google Account)**](https://docs.google.com/spreadsheets/d/1BEvN0FNI-cV6G_C72O_4tgWIL5GeA0p6Ml2j-muf5EY/copy)

### 🎯 Motivation (Bridging Civil Engineering & IT)
In marine civil engineering and surveying, weather is not just a forecast—it is a physical constraint that dictates safety and efficiency. A wave height exceeding 1.5m prevents crew transfer vessels (CTVs) from approaching turbines, and wind speeds over 10m/s make drone flights or crane operations hazardous.
This project bridges the gap between **domain knowledge of physical operations** and **IT**. It provides a real-time, 3-tier safety signal (Go / Standby / No-Go) directly to a Spreadsheet, accessible from any device including low-spec PCs or Chromebooks, without requiring complex server infrastructure.

### ✨ Features
* **Automated Data Fetching:** Periodically fetches hourly wind speed and wave height via the Open-Meteo API.
* **3-Tier Safety Logic:** Translates raw data into actionable insights:
  * 🟢 **Go (Safe):** Wind < 8.0 m/s AND Wave < 1.0 m
  * 🟡 **Standby (Caution):** Wind >= 8.0 m/s OR Wave >= 1.0 m
  * 🔴 **No-Go (Danger):** Wind >= 10.0 m/s OR Wave >= 1.5 m
* **Zero Server Maintenance:** Fully runs on Google Apps Script and Google Sheets.

### 🚀 Getting Started
1. Copy the source code `code.gs` into your Google Apps Script editor.
2. Set the target coordinates (Latitude/Longitude).
3. Set a Time-driven Trigger in GAS to run hourly.
4. Prepare a Google Sheet to act as the UI dashboard.

---

<a id="japanese"></a>
## 🇯🇵 日本語

### 🌊 概要
Google Apps Script (GAS) とスプレッドシートを活用した、洋上風力発電現場のための「実務向けマイクロ気象ダッシュボード」です。作業船の移乗やドローン点検、クレーン作業などにおける「決行（Go） / 中止（No-Go）」の判断を、局地的な風速と波高データから自動判定します。

### 📊 動作サンプル (Live Demo)
実際のダッシュボードの稼働状況を確認できます。ご自身のGoogleドライブにコピーすれば、裏側のGASコードも確認・実行可能です。
* 👁️ [**稼働中のダッシュボードを見る（閲覧のみ）**](https://docs.google.com/spreadsheets/d/1BEvN0FNI-cV6G_C72O_4tgWIL5GeA0p6Ml2j-muf5EY/edit?usp=sharing)
* 📋 [**自分のドライブにコピーしてGASを試す（要Googleアカウント）**](https://docs.google.com/spreadsheets/d/1BEvN0FNI-cV6G_C72O_4tgWIL5GeA0p6Ml2j-muf5EY/copy)

### 🎯 開発背景（土木・測量ドメインとITの融合）
測量や海洋土木の現場において、天候は単なる「予報」ではなく、作業員の命と精密機器を守るための「絶対的な物理制約」です。波高が1.5mを超えれば作業船は風車基礎に接岸できず、風速が10m/sを超えればクレーンやドローンは墜落のリスクを抱えます。
本システムは、そうした**「現場の泥臭いドメイン知識」と「IT技術」を掛け合わせた実用ツール**です。高価なサーバー構築を避け、Chromebookなどのブラウザ環境からでもサクサク確認・運用できる軽量なアーキテクチャを採用しています。

### ✨ 主な機能
* **完全自動のデータ取得:** Open-Meteo API (気象・海洋) を用い、指定座標の1時間後の風速と波高を並列取得。
* **3段階の安全判定ロジック:** 生データをそのまま見せるのではなく、現場の行動基準に落とし込みます。
  * 🟢 **安全 (Go):** 風速8m/s未満 かつ 波高1.0m未満
  * 🟡 **注意 (Standby):** 風速8〜10m/s または 波高1.0〜1.5m
  * 🔴 **危険 (No-Go):** 風速10m/s以上 または 波高1.5m以上
* **サーバーレス運用:** GASのタイムトリガーで動作し、インフラ保守ゼロ・完全無料で稼働します。

### 🚀 導入手順
1. `code.gs` をGoogle Apps Scriptエディタにコピー。
2. 監視対象の座標（緯度・経度）を設定。
3. GASの「時間主導型トリガー」で1時間おきに実行するよう設定。
4. UIとなるGoogleスプレッドシートを用意（条件付き書式で色分け推奨）。

### 👨‍💻 Author
**Masaaki Ito (伊藤 正章)**
* GitHub: [https://github.com/Masaaki-jp/](https://github.com/Masaaki-jp/)
* Blog: [むさこライフ](https://blog.hatena.ne.jp/musaco-life/) | [note](https://note.com/masa_cloud)

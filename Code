/**
 * 洋上風力マイクロ気象ダッシュボード更新スクリプト
 * 1時間後の風速と波高を取得し、スプレッドシートを更新する
 */

function updateOffshoreDashboard() {
  // 1. スプレッドシートの取得
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  
  // 2. 監視対象の座標（秋田県能代沖）
  const LAT = 40.2222;
  const LON = 139.9708;
  
  // 3. Open-Meteo APIのエンドポイント
  // ※日またぎ（23時実行時など）のエラーを防ぐため、forecast_days=2で48時間分取得する
  const weatherUrl = `https://api.open-meteo.com/v1/forecast?latitude=${LAT}&longitude=${LON}&hourly=windspeed_10m&windspeed_unit=ms&timezone=Asia%2FTokyo&forecast_days=2`;
  const marineUrl  = `https://marine-api.open-meteo.com/v1/marine?latitude=${LAT}&longitude=${LON}&hourly=wave_height&timezone=Asia%2FTokyo&forecast_days=2`;

  try {
    // 4. APIからデータを並列取得（処理速度向上のためのfetchAll）
    const responses = UrlFetchApp.fetchAll([weatherUrl, marineUrl]);
    const weatherData = JSON.parse(responses[0].getContentText());
    const marineData  = JSON.parse(responses[1].getContentText());
    
    // 5. 1時間後のデータを抽出
    const now = new Date();
    const currentHour = now.getHours();
    const targetIndex = currentHour + 1; // 1時間後のインデックス
    
    const windSpeed = weatherData.hourly.windspeed_10m[targetIndex];
    const waveHeight = marineData.hourly.wave_height[targetIndex];
    
    // 6. 3段階の作業可否判定ロジック
    let judgment = "🟢 安全 (Go)";
    
    // 波高1.5m以上 または 風速10m/s以上 は「危険」
    if (waveHeight >= 1.5 || windSpeed >= 10.0) {
      judgment = "🔴 危険 (No-Go)";
    } 
    // 波高1.0m以上 または 風速8m/s以上 は「注意」
    else if (waveHeight >= 1.0 || windSpeed >= 8.0) {
      judgment = "🟡 注意 (Standby)";
    }
    
    // 7. スプレッドシートへの書き込み
    // B1セル: 更新日時
    sheet.getRange("B1").setValue(Utilities.formatDate(now, "Asia/Tokyo", "yyyy/MM/dd HH:mm:ss"));
    // B5セル: 1時間後の風速
    sheet.getRange("B5").setValue(windSpeed);
    // B6セル: 1時間後の波高
    sheet.getRange("B6").setValue(waveHeight);
    // B8セル: 判定結果
    sheet.getRange("B8").setValue(judgment);
    
    Logger.log("ダッシュボードの更新が完了しました。");
    
  } catch (error) {
    Logger.log("エラーが発生しました: " + error.message);
    sheet.getRange("B8").setValue("⚠️ 取得エラー");
  }
}

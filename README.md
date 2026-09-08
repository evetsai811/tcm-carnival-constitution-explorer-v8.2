# 中醫嘉年華｜體質探索站 V8.3 正式版

## 上傳 GitHub Pages
請保留原 repository 內的 `assets/` 資料夾，並以本版本的以下 4 個檔案覆蓋根目錄舊檔：

- `index.html`
- `style.css`
- `script.js`
- `README.md`

圖片路徑仍沿用原本 `assets/檔名`，不需要重新上傳或修改動物圖片。

## V8.3 更新內容

1. 第一階段共 16 題，每種偏性體質由 2 題分數相加。
2. 完成第一階段後，先找出八種偏性體質的「最高分」。
3. 最高分 ≥ 6 分：僅最高分體質進入第二階段。
4. 若兩種以上體質並列最高分且 ≥ 6 分：並列最高者皆依序進入第二階段。
5. 最高分 < 6 分：直接進入平和體質第二階段。
6. 平和體質維持原有反向計分方式，≥ 60 分成立。
7. 社會人口／健康資料新增三高狀況：高血糖／糖尿病、高血壓、高血脂，可複選；「以上皆無」與前三項互斥。
8. Google Sheet 傳送版本更新為 `V8.3`。

## Google Sheet 建議欄位

依序設定：

`Timestamp | gender | ageGroup | highGlucose | hypertension | hyperlipidemia | constitution | constitutionList | version`

## Google Apps Script doGet

原本 Apps Script 也要同步新增三個三高欄位。可改為：

```javascript
function doGet(e) {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName("工作表1");
  const p = e.parameter;

  sheet.appendRow([
    new Date(),
    p.gender || "",
    p.ageGroup || "",
    p.highGlucose || "",
    p.hypertension || "",
    p.hyperlipidemia || "",
    p.constitution || "",
    p.constitutionList || "",
    p.version || "V8.3"
  ]);

  return ContentService.createTextOutput("GET success");
}
```

修改 Apps Script 後，請重新部署 Web App，並確認使用新的 `/exec` 網址（若部署網址有變更，也要同步更新 `script.js` 的 `baseUrl`）。

## 資料說明

- `highGlucose`：是／否
- `hypertension`：是／否
- `hyperlipidemia`：是／否
- 不蒐集姓名、電話等直接識別個資。

InsureGo 5.0｜零預算優先的 AI 網站部署說明

檔案結構：
index.html：完整網站
functions/api/classify.js：Cloudflare Pages Functions 後端，安全呼叫 Gemini
注意：只有上傳 HTML 無法啟用 AI；必須同時部署 functions 資料夾。

1. 在 GitHub 建立新的儲存庫，上傳 index.html 及 functions/api/classify.js（保留資料夾結構）。
2. 在 Cloudflare Dashboard → Workers & Pages → Create → Pages，連結 GitHub 儲存庫，使用 Pages 部署。
   選擇無需建置的靜態網站設定，建置輸出目錄設為根目錄（依當前 Cloudflare UI 調整）。
3. 在 Google AI Studio 取得可用的 Gemini API Key，先核對免費方案及所在地可用性。
4. Cloudflare Pages 專案 → Settings → Variables and Secrets，新增 Secret：
   GEMINI_API_KEY = 你的金鑰
   可選 GEMINI_MODEL = gemini-2.5-flash（請核對當時免費額度與可用模型）
5. 重新部署。使用 Cloudflare 提供的 pages.dev 網址，在不同裝置測試。
6. 輸入「家人住院，找不到保單」：應顯示 AI 意圖辨識；若 AI 不可用會自動退回規則式備援。

安全與限制：
- 不要把金鑰寫在 HTML、GitHub 程式碼或聊天訊息中。
- 這份示範版沒有持久化使用者輸入，也不連結真實保單；AI 問題會傳送至第三方模型服務。
- 不要輸入姓名、電話、身分證、保單號碼、病歷或其他敏感個資。
- 後端有基本輸入限制，但尚未加入每人頻率限制；公開評審測試前，建議設定 Cloudflare WAF / Rate Limiting 防濫用規則。
- AI 只分類需求，知識庫目前仍是示範資料；正式規定與網址需等待隊友核實後整合。
- 免費額度、Cloudflare 部署介面與 Gemini 模型名稱可能變更；若不適用請改用當時可用模型。
- 本機雙擊 index.html 時，API 不會運作，但備援導航仍可操作。

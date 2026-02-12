---
name: higgsfield-nano-banana
description: Commands OpenClaw bot to generate images on Higgsfield using nano_banana_2; supports prompts from StarScene Pro history (click last record, iterate 5–15 items per record) or from prompts.txt. Always enables Unlimited on Higgsfield to avoid consuming site Credit. Use when user asks for Higgsfield image generation, StarScene Pro, nano_banana_2, batch prompts, or saving credits.
metadata: {"openclaw":{"requires":{"config":["browser.enabled"]},"emoji":"🍌"}}
---

# Higgsfield Nano Banana 2 圖片產生

讓 OpenClaw bot 在 Higgsfield 網站上使用 **nano_banana_2** 模型產生圖片，並**一律先點擊 Unlimited**，避免消耗網站 Credit。支援兩種 Prompt 來源：**StarScene Pro 歷史記錄**（點擊上一個記錄、逐條投放該記錄內 5~15 筆資料）或本機 **prompts.txt**。

## 必要前提

- 已啟用 OpenClaw 的 **browser** 工具（`browser.enabled: true`）。

**來源選擇**：若使用者提到「StarScene Pro」「歷史記錄」「上一個記錄」「starscene-new.vercel.app」或從網頁取得 prompt，使用**來源 A**；若僅提供本機檔案或 `prompts.txt`，使用**來源 B**。

---

## 來源 A：從 StarScene Pro 歷史記錄投放

當使用者要求「從 StarScene Pro 歷史記錄投放到 Higgsfield」或「點擊上一個記錄投放」時，依下列流程操作。

### 1. 開啟 StarScene Pro 並找到歷史記錄

- 使用 `browser`：`navigate` 至 **https://starscene-new.vercel.app/**（StarScene Pro | AI 電影場景生成器）。
- 待頁面載入後 `snapshot`，找到右側 **「歷史記錄」** 區塊（通常顯示「歷史記錄 10」等數字，表示筆數）。
- 點擊**上一筆／最新一筆**歷史記錄（列表中最上方那一條，例如「寶可夢 #4批次」之類的標題）。點擊後主內容區會顯示該筆記錄的詳情。

### 2. 辨識該記錄下的多條資料（5~15 條）

- 單一筆「歷史記錄」底下常對應**多條** HIGGSFIELD PROMPT（例如 5~15 條）。詳情頁可能以：
  - 單一區塊「HIGGSFIELD PROMPT (9:16)」顯示一條，並有切換/下一條控制；或
  - 列表/分頁顯示多條；或
  - 需點擊「下一條」或索引才切換到下一則 prompt。
- 用 `snapshot` 確認：當前可見的 **HIGGSFIELD PROMPT** 文字、以及是否有「下一條」「下一筆」、索引（如 1/15）或列表可點。
- **目標**：依序取得該記錄下的**每一條** Higgsfield Prompt，準備逐條投放到 Higgsfield。

### 3. 逐條投放到 Higgsfield（每條都先 Unlimited 再 Draw）

對**該記錄內的每一條資料**重複以下步驟，直到全部投放完畢：

1. **取得當前條的 Prompt 文字**
   - 從主內容區的「HIGGSFIELD PROMPT (9:16)」區塊取得完整 prompt 文字（必要時可點「複製」按鈕再於 Higgsfield 貼上，或從 snapshot 中讀取文字）。

2. **前往 Higgsfield**
   - 可點擊頁面上的 **「前往 Higgsfield」** 按鈕（橙色）直接跳轉，或 `navigate` 至 `https://higgsfield.ai/image/nano_banana_2`。
   - 若已在 Higgsfield 分頁，可 `focus` 該分頁或新開分頁後再 navigate。

3. **在 Higgsfield 產生這一張圖**
   - **先啟用 Unlimited**：在 Higgsfield 介面上點擊/切換 **Unlimited**（切換開關或螢光綠 Unlimited 按鈕），確保不消耗 Credit。
   - 在 **prompt 輸入框**貼上/輸入當前這一條的 prompt。
   - 點擊 **Draw** 開始產生。
   - 依需要等待產生完成（可 `snapshot` 或 `wait`），再進行下一條。

4. **下一條**
   - 回到 StarScene Pro 分頁（或重新 navigate 到該記錄詳情頁）。
   - 若介面有「下一條」「下一筆」或索引，點擊以切換到下一則 HIGGSFIELD PROMPT；若無，依 snapshot 判斷如何切換（例如列表點擊、分頁等）。
   - 重複上述「取得 prompt → 前往 Higgsfield → Unlimited → 貼上 → Draw」直到該記錄下所有條目（5~15 條）都投放完畢。

### 4. 注意事項（StarScene Pro）

- 每個「歷史記錄」對應多條資料時，**必須輪流、逐個投放**，不要只投第一條就結束。
- 若使用者指定「上一個記錄」以外的記錄，則改為點擊該筆記錄後，同樣依上述方式辨識並逐條投放該筆記錄內的所有條目。

---

## 來源 B：從本機 prompts.txt 投放

當使用者提供或已存在本機記錄檔（例如 `prompts.txt`）時使用此流程。

## 工作流程（本機 prompts）

1. **開啟瀏覽器並前往 Higgsfield nano_banana_2 頁面**
   - 使用 `browser` 工具：`navigate` 至 `https://higgsfield.ai/image/nano_banana_2`（或當前官方 nano_banana_2 圖片產生頁面）。
   - 若頁面需載入，可先 `snapshot` 確認介面已出現。

2. **每次產生前：務必啟用 Unlimited**
   - 在 Higgsfield 介面上會有「Unlimited」相關控制：
     - **Unlimited 切換/按鈕**：可能是切換開關（toggle）或明顯的「Unlimited」按鈕（例如螢光綠按鈕）。
   - **每次**要點擊「Draw」產生圖片**之前**，必須先：
     - 點擊或切換至 **Unlimited**，確保目前使用的是「Unlimited Nano Banana Pro」配額，**而不是**網站的 Credit。
   - 若 snapshot 中看到多個「Unlimited」元素（例如一個在數量旁、一個較大的主按鈕），優先點擊**明確代表「使用無限方案」**的那一個（常是較大、顯眼的主 Unlimited 按鈕），或將切換開關設為開啟。
   - 若無法從 snapshot 判斷，則兩個 Unlimited 相關控制都確保為「已選中/已開啟」再進行產生。

3. **依本機記錄檔投放產生**
   - 從使用者指定或預設的記錄檔（例如 `prompts.txt` 或 `{baseDir}/prompts.txt`）讀取 prompt 列表（每行一則或依約定格式）。
   - 對**每一則** prompt：
     - 在 Higgsfield 網頁的 **prompt 輸入框**中填入該則文字（必要時先清空再輸入）。
     - 再次確認 **Unlimited** 已啟用（若同頁有多個 Unlimited 控制，確保代表「無限方案」者為 ON）。
     - 點擊 **Draw**（繪製）按鈕開始產生。
     - 依需要等待產生完成（可 `snapshot` 或 `wait` 觀察結果），再進行下一則或下載結果。

4. **可選**
   - 若使用者需要下載圖片，在每次產生完成後用 snapshot 找到下載或儲存按鈕並操作。
   - 若有多張（例如 1/4+ 數量設定），可依介面設定數量後再按 Draw；仍以**先設 Unlimited** 為優先。

## 重要提醒

- **未點擊 Unlimited 就按 Draw，會消耗網站 Credit。** 因此流程中必須把「先啟用 Unlimited」當作固定步驟，不可省略。
- 若介面改版，以「Unlimited」文字或明顯的無限方案切換/按鈕為準，必要時用 `browser snapshot` 再確認元素位置與 ref，再執行 `click`。

## 本機記錄的 Prompts 來源（來源 B 專用）

- 預設可讀取 `{baseDir}/prompts.txt`（與本 skill 同目錄），每行一則 prompt；以 `#` 開頭的行可視為註解並略過。
- 範例檔：`{baseDir}/prompts.example.txt`，可複製為 `prompts.txt` 後編輯。
- 若使用者提供其他路徑或檔案名，從該檔案讀取並依相同流程：每則 prompt → 確保 Unlimited → 輸入 prompt → 點擊 Draw。

## 參考 URL

- **StarScene Pro**（歷史記錄來源）：https://starscene-new.vercel.app/
- **Higgsfield Nano Banana 2**：https://higgsfield.ai/image/nano_banana_2

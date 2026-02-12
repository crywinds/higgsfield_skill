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

## Higgsfield 網頁操作細節（必讀）

在 Higgsfield 頁面上產生圖片時，必須依**固定順序**操作以下三個目標元素。網站可能使用隨機 class 或 ID 防機器人，因此**一律用語意方式辨識**（role、name、placeholder、可見文字），不要依賴 class 或動態 ID；snapshot 後用描述比對 ref 再操作。

### 1. 將 Prompt 貼到輸入框

- **目標**：多行文字輸入框（textarea），用於輸入場景描述。
- **辨識方式**（任一種符合即可）：
  - `name="prompt"` 的輸入框；
  - 或 placeholder 為 **"Describe the scene you imagine"** 的 textarea；
  - 或 snapshot 中角色為 textbox、且標籤/placeholder 與「場景描述」相關的那一個。
- **操作**：對該 ref 使用 `type`（或 `fill`）將當前要產生的 **prompt 全文**貼上；必要時先清空再輸入。不要依賴該元素的 class 或隨機屬性。

### 2. 開啟 Unlimited 開關（必須為 ON）

- **目標**：一個**切換開關**（switch），控制是否使用 Unlimited 方案。若為關閉狀態，會消耗網站 Credit。
- **辨識方式**：
  - 角色為 **switch**（`role="switch"`）的按鈕；
  - 若 snapshot 顯示 `aria-checked="false"` 或「off」/「未選中」，表示尚未開啟，**必須點擊一次**使其變為 `aria-checked="true"`（ON）。
- **操作**：在 snapshot 中找到對應該 switch 的 ref，執行 `click`。若 snapshot 顯示已為「on」/「checked」可略過；否則**每次產生前都先確認此開關為開啟**。

### 3. 點擊「Unlimited」按鈕

- **目標**：顯示文字 **"Unlimited"** 的按鈕或可點擊區塊（旁邊可能有小星星/閃光圖示）。這是正式啟用「Unlimited」方案的操作，與上述開關不同。
- **辨識方式**：
  - 在 snapshot 中找**可見文字為 "Unlimited"** 的按鈕或連結；
  - 可能以 "Unlimited" 加上圖示或數字（如 "Unlimited 2"）出現，選主「Unlimited」控制即可。
- **操作**：對該 ref 執行 `click`。**每次要按 Draw 之前都要先完成此步驟**（連同步驟 2 的開關為 ON）。

### 4. 操作順序與 Draw

在 Higgsfield 上**每次**產生一張圖的建議順序：

1. 在 **prompt 輸入框**（步驟 1）貼上/輸入當前 prompt；
2. 確認 **Unlimited 開關**（步驟 2）為**開啟**，若為關閉則點擊一次；
3. 點擊 **"Unlimited"** 按鈕/區塊（步驟 3）；
4. 點擊 **Draw**（繪製）按鈕開始產生。

### 抗隨機化：如何穩定辨識元素

- 網站可能為防機器人而使用**隨機或動態的 class / ID**，因此：
  - **不要**依賴 `class`、`id` 或 data 屬性來選元素；
  - **要**依賴：**role**（如 switch、textbox）、**name**（如 prompt）、**placeholder** 文字（如 "Describe the scene you imagine"）、**可見文字**（如 "Unlimited"、"Draw"）、**aria-checked** 等語意或可訪問性資訊。
- 每次 `browser snapshot` 後，根據上述描述在 snapshot 輸出中對應到正確的 ref（數字或 role ref 如 e12），再對該 ref 執行 `click` 或 `type`。若一頁有多個相似元素，以「與 prompt 輸入／Unlimited 開關／Unlimited 按鈕」語意最相符者為準。

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

3. **在 Higgsfield 產生這一張圖**（嚴格依「Higgsfield 網頁操作細節」一節順序）
   - 在 **prompt 輸入框**（辨識：name=prompt 或 placeholder "Describe the scene you imagine"）貼上當前這一條的 prompt；
   - 將 **Unlimited 開關**（role=switch）點擊為**開啟**（aria-checked=true）；
   - 點擊顯示 **"Unlimited"** 文字的按鈕；
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

2. **每次產生前：依「Higgsfield 網頁操作細節」操作**
   - 對每一則 prompt：先將文字貼到 **prompt 輸入框**（name=prompt 或 placeholder "Describe the scene you imagine"）；再將 **Unlimited 開關**（role=switch）點為開啟；再點擊 **"Unlimited"** 按鈕；最後點擊 **Draw**。不可省略或調換順序。

3. **依本機記錄檔投放產生**
   - 從使用者指定或預設的記錄檔（例如 `prompts.txt` 或 `{baseDir}/prompts.txt`）讀取 prompt 列表（每行一則或依約定格式）。
   - 對**每一則** prompt：依上方的「Higgsfield 網頁操作細節」順序操作（輸入框 → Unlimited 開關 ON → Unlimited 按鈕 → Draw），並以 **role/name/placeholder/可見文字** 辨識元素，不依賴 class 或隨機 ID。
     - 依需要等待產生完成（可 `snapshot` 或 `wait` 觀察結果），再進行下一則或下載結果。

4. **可選**
   - 若使用者需要下載圖片，在每次產生完成後用 snapshot 找到下載或儲存按鈕並操作。
   - 若有多張（例如 1/4+ 數量設定），可依介面設定數量後再按 Draw；仍以**先設 Unlimited** 為優先。

## 重要提醒

- **未將 Unlimited 開關開啟並點擊 Unlimited 按鈕就按 Draw，會消耗網站 Credit。** 每次產生前必須依「Higgsfield 網頁操作細節」完成：輸入框 → 開關 ON → Unlimited 按鈕 → Draw。
- 元素可能帶隨機 class/ID：**只用 role、name、placeholder、可見文字**在 snapshot 中對應 ref，再 `click`/`type`，不要依賴 class 或 id。

## 本機記錄的 Prompts 來源（來源 B 專用）

- 預設可讀取 `{baseDir}/prompts.txt`（與本 skill 同目錄），每行一則 prompt；以 `#` 開頭的行可視為註解並略過。
- 範例檔：`{baseDir}/prompts.example.txt`，可複製為 `prompts.txt` 後編輯。
- 若使用者提供其他路徑或檔案名，從該檔案讀取並依相同流程：每則 prompt → 確保 Unlimited → 輸入 prompt → 點擊 Draw。

## 參考 URL

- **StarScene Pro**（歷史記錄來源）：https://starscene-new.vercel.app/
- **Higgsfield Nano Banana 2**：https://higgsfield.ai/image/nano_banana_2

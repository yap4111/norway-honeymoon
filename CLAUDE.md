# 新婚計劃 — 挪威極光蜜月計劃書 專案規範

每個 session 接手本專案前，先讀本檔與 `規劃總覽.md`，並遵循以下規範。

## 專案目的與主檔

- **主交付物**：`挪威極光蜜月_完整計劃書.html`（整合主檔，一頁到底）。`index.html` 只是轉址，內容別寫在它裡面。
- **線上發布**：GitHub Pages（**個人帳號 yap4111**，非公司 NaturalVegetarian）→ <https://yap4111.github.io/norway-honeymoon/>。**改完必須 commit + push 才會更新線上版**；回報時提醒對方手機重整。
- **行程骨幹**：2027/2/26 出發–3/14 返。奧斯陸 2 + Tromsø 4 + Bodø 1（防火牆）+ Lofoten 6 + 奧斯陸 1（緩衝夜）。國際/國內機票皆已訂（海航經北京；國內 SAS/Widerøe）。
- **使用者**：要帶女友一起看、一起規劃；蜜月行，語氣可溫暖。

## 核心規劃原則（這份文件的「個性」）

- **不替使用者拍板**：還沒定的事用「方案 A/B/C」並列、保留選擇權；只給建議與理由。
- **誠實面對不確定**：極光、天氣、船班、營業時間都不保證 → 明講「不保證/季節休/易停航」。寧可標「待確認」也不要假裝確定。
- **概值要標示**：光線時刻、傍晚藍調時段、車程、價格一律標「概值・行前以官網 / timeanddate.com / yr.no 核對」。**絕不假精確**（尤其不要把估算的藍調時刻寫成精確時間）。
- **已訂 vs 待訂分清楚**：已訂用 ✅ + 實際金額；待訂用預估區間。金額/座標/班機**以檔案現況為準**，查證後才更新，別憑印象改。
- **省錢主軸**：郊區晚餐自炊（挪威外食貴、優先有廚房房型）；酒只在 Vinmonopolet（週日休）。
- **租電動車**：每個地點都評估「停車便利性 + 是否有充電樁 + 要不要在此充」。策略固定為「**住處慢充過夜 + 城鎮（Leknes/Svolvær/Tromsø）過路快充**」，景點/海灘多半無快充。

## 地圖 pin 規範（最容易出錯、最重要）

- 標準格式：
  ```html
  <a class="pin" target="_blank" rel="noopener" href="https://www.google.com/maps/search/?api=1&amp;query=QUERY">📍</a>
  ```
- **HTML 屬性內 `&` 一律寫 `&amp;`**（對齊既有寫法）。
- `QUERY` 用 URL-encoded 文字；**住宿、落點不明確、同名易混的地點一律改用座標 `lat,lng`**。
- **每個 pin 都要查證會落到對的地方**，常見坑：
  - 同名異地（Hella、Storvatnet 等泛用名）→ 改具體 POI 或座標。
  - 品牌改名（Best stasjon → YX）→ 用現名。
  - 純地名/泛稱（`strand`、`beach`、整座漁村）落點太廣 → 改精確座標或具體 POI（如 Arctic Hotel）。
  - 文字 query 偶爾 Google 不認（例：`Sommarøybrua`）→ 改座標（69.6236,18.0456）。
- **逐日時間表**：每個「有導航目的地」的列都加 📍；非導航列（自炊/退房/加滿油/起飛）不加；同一地名同一天只加一次。
- **住宿一覽表**：每列住宿名後加 📍（用該住宿座標）。
- 解 Google Maps 短連結（goo.gl）：用 **WebFetch**，302 redirect 的 URL 會帶 `@lat,lng` 與 `!3d/!4d`，取座標。
- 不確定就用 **WebSearch 查證**，並在文案保留「概值/行前確認」。曾做過整批 pin 查證 workflow（45 個 pin），值得沿用。

## HTML 結構與樣式慣例

- **section id 與 nav 連結要同步**：`flights / tw / days / tromso / lofoten / maps / aurora / budget / pack / timeline / check`（已刪除 `drive`、`stay`：自駕內容併入 lofoten、住宿推薦章已移除）。
- **CSS class 語意，別混用**：
  - `note` = 硬限制 / 不可變更前提；`warn` = 安全 / 待確認；`gold` = 關鍵結論 / 重點提醒；`seg` = 分區標頭。
  - 逐日卡：`.day > .dhead(.ddate .dtitle .flag) > scroll-x>table > .dmeta`。
  - 其他：`.opt .nightline .chips .chip(.ok/.x) .card .sec-head .sec-ico .pin .phone .tocard`。
- **逐日 seg 放當地代表縮圖** `<img class="segimg" src="images/X.jpg">`；**專題 seg（電量/住宿/健行/該先訂/地圖/停車充電）不放圖**。
- **圖檔在 `images/`**：`nor-*`、`west-*`、`master-*` 是本趟挪威圖；`ch-/gr-/it-/tr-/no-` 是別專案模板，**別用**。用圖前確認檔名存在，且**別把 Lofoten 的圖放到 Tromsø 的天**（曾誤用 `west-hamnoy.jpg` 在 Tromsø Day2）。
- **Tromsø 5 日與 Lofoten 6 日「呈現方式要對齊」**，統一模板順序：
  `sec-head → note 硬限制 → 住宿價格表(偏上) → 光線時間表(4 欄:日期/日出/日落/傍晚藍調(最美)) → 逐日(seg+day，連續、中途不插主題卡) → 🔋電量 → 🏡住宿訂房明細 → 🥾健行 → 🍽餐食&海鵰(Lofoten) → 🐟慢遊表 → 📏距離表 → 📋該先訂 → 📍地圖速查 → 🅿停車/充電/購票 → ❄冬季自駕 → ⚠全段提醒`。

## 改檔 / 驗證 / 發布流程

- **大改前先完整讀檔**掌握結構（檔約 1000+ 行）。
- **大型結構重整**（刪併區段、跨段對齊、批量加連結）：可用 **Workflow** 做「分析 > 評估 > 提方案 > 收攏」（並行讀取分析 + 收攏代理，輸出 JSON 計畫），再由主程式**親手套用編輯**（別讓多代理同時寫同一檔）。
- **刪整段**用 `sed '起,迄d'` 行範圍刪除最穩（避免巨大 old_string 易失敗）；刪後檢查 `<div class="divider">❄ ❄ ❄</div>` **不要連續重複**。
- **每次改完必驗證**（Bash + grep）：
  - `<div>` 開合數量平衡、`<table>` 開合平衡。
  - 無殘留壞 query、無已刪區段的舊錨點（`href="#drive"`、`href="#stay"`）。
- **git**：本地已設 `user.name "NaturalVegetarian"` / `user.email nv20190522@gmail.com`；push 走個人 **yap4111** 憑證（公司 workhub repo 的 GCM 帳號別動）。**commit message 用繁中**（保留英文術語），結尾加 `Co-Authored-By: Claude ...`。
- 改完 **commit + push**，回報網址並提醒手機重整。

## 溝通

- 全程**繁體中文（台灣用語）**；檔案路徑、指令、原文錯誤訊息不翻譯。
- 既有事實（已訂金額、座標、班機、訂房）以檔案為準；查證後才更新，不憑印象改。

## 相關檔案

- `規劃總覽.md`：專案總覽（接手前先讀）。
- `費用紀錄.md`：帳本（已訂金額同步來源）。
- `封存_舊版與細節/`：整合前的原始細節檔（西 Lofoten 深度、每晚住宿選擇、3 月極光總覽），留作對照。

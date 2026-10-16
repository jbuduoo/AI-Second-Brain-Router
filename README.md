# AI Second Brain Router

> A lightweight context-routing system for your personal AI.

AI Second Brain Router 是一套讓 AI 能持續理解你的專案、資料位置與歷史記錄的簡單架構。

核心不是把所有資料一次塞進 Context，而是讓 AI 依目前問題判斷：**這次需要什麼資料、資料在哪裡、是否真的需要讀取。**

## 核心概念

```text
使用者提問
    ↓
自訂指令：告訴 AI 從哪裡開始
    ↓
AI_RULES：判斷這次真正需要什麼資料
    ↓
需要時才讀取 Project Index / Google Drive / 歷史記錄 / Calendar / Gmail / GitHub
    ↓
整理回答，並顯示實際資料路由
```

## 主要功能

- **專案延續**：跨對話查詢專案進度、決策、規格與待辦。
- **資料導航**：透過 Project Index 找到正確的 Google Drive、GitHub 或其他資料來源。
- **按需讀取**：不把所有歷史資料一次載入 Context。
- **歷史檢索**：先從 Summary 找候選記錄，需要原始上下文時才讀 Raw。
- **明確存檔**：只有使用者明確要求「存檔」時才建立記錄。
- **來源透明**：回答可顯示實際讀取來源與資料路由。
- **服務擴充**：可依需求連接 Google Calendar、Gmail、GitHub 等服務。

## V1 檔案

```text
README.md
AI_RULES.md
custom-instructions.example.md
project-index.example.csv
```

這四個檔案就是最小可運作版本。

## 使用需求

你需要一個能支援以下能力的 AI 環境：

- 自訂指令或等效的固定入口設定
- Google Drive 或其他檔案來源連接能力
- 需要時可讀取文件、試算表與專案資料
- 若要讓 AI 寫入記錄，必須具備相對應的寫入權限

Google Calendar、Gmail、GitHub 都是選配；有明確使用情境時再連接即可。

## 快速開始

1. 在 Google Drive 建立一個第二大腦根目錄。
2. 將 `AI_RULES.md` 的內容建立成 AI規則文件。
3. 依 `project-index.example.csv` 建立自己的 Project Index。
4. 複製 `custom-instructions.example.md` 到 AI 的自訂指令。
5. 將 `<YOUR_SECOND_BRAIN_FOLDER_URL>` 替換成自己的第二大腦資料夾網址。
6. 連接 Google Drive，確認 AI 可以讀取 AI規則。
7. 依需求連接 Google Calendar、Gmail、GitHub。
8. 執行下方驗收測試。

## Project Index

Project Index 是整套架構的導航表，不是知識庫本身。

建議欄位：

- 專案名稱
- 別名 / 關鍵字
- GitHub
- Google Drive
- 本機位置
- 狀態
- 備註

AI 只有在需要專案資料、但不知道資料位置或無法確認專案時，才應查詢 Project Index。

## 每個專案最低需要什麼

每個專案不需要固定的複雜模板。最低只需要：

- 在 Project Index 有一列。
- 有至少一個資料來源位置，例如 Google Drive 或 GitHub。
- 若要保存歷史對話，可在專案內建立「記錄」資料夾。
- 若專案有特殊規則，可放 README、專案說明或注意事項。

## 記錄格式

每次存檔建立一份記錄，包含兩層：

### Summary

用於未來快速搜尋與接續，可整理：

- 重要結論
- 決策
- 規格
- 進度
- Bug 與解法
- 未完成事項
- 後續工作

### Raw

保存本次存檔範圍內的原始對話，不摘要、不改寫、不刪減。

Summary 是搜尋層；Raw 是原始資料層。

## 權限與隱私原則

- Repo 中只放**範本**，不要放自己的真實 Project Index。
- 不要公開私人 Google Drive Folder ID、本機帳號路徑、Email、姓名或客戶資料。
- 採取最小權限：只需要讀取的來源只給讀取權限；確定需要寫入時才開啟寫入權限。
- AI 應只讀取完成目前任務真正需要的資料。
- 建議將真實設定保留在私人 Drive，GitHub 只保存可複製的公開範本。

## 驗收測試

至少測試：

1. 新開對話後，AI 能讀到 AI規則。
2. 問一般問題時，不會不必要地查 Project Index 或 Drive。
3. 問已知專案時，能使用正確的專案資料。
4. 不知道專案位置時，才查 Project Index。
5. 查歷史決策時，優先讀 Summary，必要時才讀 Raw。
6. 明確說「存檔」時，能在正確專案建立記錄。
7. 回答結尾能正確顯示實際資料路由。
8. 若啟用其他連接器，可正確讀取相對應來源。

## 使用範例

```text
「Sample Project 目前做到哪？」
「找出之前討論過的登入規格。」
「我目前有哪些未完成事項？」
「我明天下午有什麼行程？」
「找出某封 Email 裡的決策。」
「存檔。」
```

## V1 範圍

V1 專注在一件事：**讓 AI 知道去哪裡找資料，而不是把所有資料都塞進 Context。**

未來版本可以再加入更完整的待辦管理、摘要檢索、自動化與跨服務整合。
